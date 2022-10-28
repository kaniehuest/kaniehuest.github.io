---
title: Hack The Boo 2022 - Evaluation Deck
layout: post
description: La resolución del reto "Spookifier" del CTF "Hack The Boo 2022" organizado por Hack The Box.
tags:
- HackTheBox
- Spookifier
- HackTheBoo
- ctf
- post
- writeups
---
# Descripción
---

There's a new trend of an application that generates a spooky name for you. Users of that application later discovered that their real names were also magically changed, causing havoc in their life. Could you help bring down this application?

# Solución
---

El segundo reto web del CTF nos presenta un campo input y un botón. 

![](/images/images-hacktheboo2022/spookifier-1.png)

Podemos introducir texto.

![](/images/images-hacktheboo2022/spookifier-2.png)

Al presionar el botón, la aplicación nos responde con el mismo texto pero con la fuente cambiada.

![](/images/images-hacktheboo2022/spookifier-3.png)

Por suerte tenemos el código fuente para ayudarnos. Empezando con el archivo **Dockerfile** notamos que la flag está ubicada en `/flag.txt`, esta información nos servirá más adelante.

![](/images/images-hacktheboo2022/spookifier-4.png)

Leyendo los archivos del reto vemos un posible SSTI en la función `generate_render()`.

![](/images/images-hacktheboo2022/spookifier-5.png)

No es necesario hacer pruebas para detectar el motor de templates porque tenemos el código fuente, en este caso se está usando `Mako`.

![](/images/images-hacktheboo2022/spookifier-6.png)

Buscando maneras de explotar un SSTI con Mako nos encontramos con PayloadAllTheThings [Link de los payloads](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection#mako), copiamos el primer payload que nos muestra PaloadAllTheThings y lo pegamos en el input de la página.

```perl
${self.module.cache.util.os.system("id")}
```

![](/images/images-hacktheboo2022/spookifier-7.png)

Notamos que las letras de nuestro payload cambian de fuente en las primeras 3 respuestas, pero en la última nuestro payload se ejecuta y nos devuelve un 0 como respuesta.

![](/images/images-hacktheboo2022/spookifier-8.png)

Esta ocurre porque cuando enviamos nuestra cadena de texto, las primeras 3 veces cada letra cambia de fuente por separado y al momento de juntarse y renderizarse nuestro payload ya no tiene sentido, esto hace que ya no sea "una inyección de código" válida. Lo que pasa en la cuarta respuesta es que las letras no cambian de fuente, nuestro payload final no tiene problemas al renderizarse y así explotamos un SSTI.

![](/images/images-hacktheboo2022/spookifier-9.png)

Cambiamos el comando que utilizamos por uno que nos sirva para visualizar la flag.

```perl
${self.module.cache.util.os.system("cat /flag.txt")}
```

Pero nos devuelve un 0, imagino que este número es el código de salida del comando.

![](/images/images-hacktheboo2022/spookifier-10.png)

Para estar seguro escribiremos un comando que no existe y esperamos que el código de salida sea un númera más alto que 0.

```perl
${self.module.cache.util.os.system("abcd")}
```

![](/images/images-hacktheboo2022/spookifier-13.png)

Y confirmamos, esto solo nos devuelve el código de salida.

![](/images/images-hacktheboo2022/spookifier-14.png)

En la página de HackTricks existe una gran cantidad de payloads que pueden servir para explotar este SSTI, yo voy a probar este que simplemente abre un archivo y lo lee, pero vamos a modificarlo para que nos muestre la flag.
[Link de la página de HackTricks](https://book.hacktricks.xyz/generic-methodologies-and-resources/python/bypass-python-sandboxes).

```python
open("/flag.txt").read()
```

![](/images/images-hacktheboo2022/spookifier-17.png)

Nuestro payload se ejecuta correctamente y obtenemos la flag.

![](/images/images-hacktheboo2022/spookifier-18.png)

# Flag
---

`HTB{t3mpl4t3_1nj3ct10n_1s_$p00ky!!}`
