---
title: PortSwigger - Blind SQL injection with conditional responses
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Blind SQL injection with conditional responses. 
tags:
- portswigger
- sqli
- post
- writeups
---
# Solución
---

Ingresamos al laboratorio.

![](/images/images-portswigger-sqli/lab11-1.png)

Para resolver este laboratorio utilizaré Burpsuite Professional porque realizaremos un ataque de fuerza bruta, y si realizamos este ataque con el Burpsuite Community tardaremos un año entero. Es posible utilizar otras herramientas de fuzzing como FFuF o wfuzz O..... puedes programar un script en tu lenguaje de programación favorito que realice el ataque de fuerza bruta como hice yo [acá](https://github.com/kaniehuest/PortSwigger-autoPWN).


Primero configura la extensión [FoxyProxy](https://getfoxyproxy.org/) para que funcione con Burpsuite, después ve a Burpsuite y haz click en el botón **Intercept is off** para que quede en azul.

![](/images/images-portswigger-sqli/lab11-2.png)

![](/images/images-portswigger-sqli/lab11-3.png)

Luego vuelves a la página principal y recargas la página para interceptar la petición.

![](/images/images-portswigger-sqli/lab11-4.png)

Cuando interceptes la petición debe hacer click derecho y seleccionar la opción **Send to Repeater**.

![](/images/images-portswigger-sqli/lab11-5.png)

Vas a la pestaña Repeater.

![](/images/images-portswigger-sqli/lab11-6.png)

Y nos vamos a enfocar en la cookie TrackingId.

![](/images/images-portswigger-sqli/lab11-7.png)

Hacemos click en el botón **Send** y vemos la respuesta.

![](/images/images-portswigger-sqli/lab11-8.png)

Como nos indica la descripción del reto, el mensaje **Welcome back!** nos permitirá saber si nuestra petición es correcta o no.

![](/images/images-portswigger-sqli/lab11-9.png)

Por ejemplo, si agregamos una comilla a la cookie el mensaje **Welcome back!** no aparece en la página.

![](/images/images-portswigger-sqli/lab11-10.png)

Si agregamos `' and 1=1-- -` volvemos a tener el mensaje.

![](/images/images-portswigger-sqli/lab11-11.png)

Escribimos `' AND (SELECT '' FROM users)=''-- -` con el fin de comprobar que la tabla users exista. Acá comparamos `SELECT '' FROM users` (debería devolvernos un string vacía) con `''` (una string vacía), pero nos da un error.

![](/images/images-portswigger-sqli/lab11-12.png)

Esto es porque la query `SELECT '' FROM users` nos devuelve más de 1 resultado, para indicarle que queremos solo 1 resultado agregamos `LIMIT 1`.

```SQL
' AND (SELECT '' FROM users LIMIT 1)=''-- -
```

Y obtenemos el mensaje.

![](/images/images-portswigger-sqli/lab11-13.png)

Ahora comprobamos que el usuario administrator exista. Acá ejecutamos `SELECT '' FROM users WHERE username='administrator'`, si la petición es correcta entonces nos devolverá una string vacía, y si la comparamos con otra string vacía deberíamos ver el mensaje **Welcome back!**. Si no existe el usuario administrator entonces la comparación falla y no deberíamos ver el mensaje.

```SQL
' AND (SELECT '' FROM users WHERE username='administrator')=''-- -
```

![](/images/images-portswigger-sqli/lab11-14.png)

Como ya comprobamos que el usuario administrator existe, ahora enumeraremos el largo de su contraseña agregando `AND LENGTH(password) > 0`. Si el largo de la contraseña el mayor a 0 entonces deberíamos ver el mensaje **Welcome back!**, de lo contrario no deberíamos ver el mensaje.

![](/images/images-portswigger-sqli/lab11-15.png)

No tenemos idea del largo de la contraseña, podría ser de 5 o de 80 caracteres. Usaremos el Intruder para automatizar esta enumeración.

Hacemos click derecho sobre la petición y seleccionamos la opción **Send to Intruder**.

![](/images/images-portswigger-sqli/lab11-16.png)

Hacemos click en el botón **Clear**.

![](/images/images-portswigger-sqli/lab11-17.png)

Marcamos el número 0.

![](/images/images-portswigger-sqli/lab11-18.png)

Y hacemos click en el botón **Add**.

![](/images/images-portswigger-sqli/lab11-19.png)

Debería verse así.

![](/images/images-portswigger-sqli/lab11-20.png)

Luego vamos a la pestaña **Payloads**, seleccionamos la opción **Numbers** en la pestaña Payload type, y en Payload Options seleccionamos **From: 1**, **To: 80** y **Step: 1**

![](/images/images-portswigger-sqli/lab11-21.png)

Hacemos click en el botón **Start attack** para comenzar el ataque de fuerza bruta.

![](/images/images-portswigger-sqli/lab11-22.png)

Mientras se ejecuta el ataque vamos a la pestaña **Options**.

![](/images/images-portswigger-sqli/lab11-23.png)

Al final vemos la opción **Grep-Match**.

![](/images/images-portswigger-sqli/lab11-24.png)

Hacemos click en **Clear**.

![](/images/images-portswigger-sqli/lab11-25.png)

Escribimos **Welcome back!** y hacemos click en el botón **Add** para que filtre por esa frase.

![](/images/images-portswigger-sqli/lab11-26.png)

Volvemos a la pestaña **Results**.

![](/images/images-portswigger-sqli/lab11-27.png)

Y notamos que la contraseña es mayor que 19 pero no es mayor que 20. Esto significa que la contraseña de administrador tiene 20 caracteres.

![](/images/images-portswigger-sqli/lab11-28.png)

Volvemos a la pestaña Repater y cambiamos nuestra query.

```SQL
' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a'-- -
```

En esta nueva query comparamos la primera letra de la contraseña del administrador (`SUBSTRING(password,1,1)`) con la letra **a** (`='a'`).

![](/images/images-portswigger-sqli/lab11-29.png)

Como no vemos el mensaje entonces la primera letra de la contraseña no es **a**.

![](/images/images-portswigger-sqli/lab11-30.png)

Según el Hint del laboratio, la contraseña del admin puede contener letras maýusculas, letras minúsculas y números, si intentamos enumerar a mano nos demoraremos 3 años, así que enviaremos la petición al Intruder. 

![](/images/images-portswigger-sqli/lab11-31.png)

Hacemos click en **Clear**.

![](/images/images-portswigger-sqli/lab11-32.png)

Seleccionamos el primer número 1 y hacemos click en **Add**.

![](/images/images-portswigger-sqli/lab11-33.png)

Después seleccionamos la letra `a` y hacemos click en **Add**.

![](/images/images-portswigger-sqli/lab11-34.png)

En **Attack type** seleccionamos **cluster bomb**.

![](/images/images-portswigger-sqli/lab11-35.png)

Y nos vamos a la pestaña **Payloads**.

![](/images/images-portswigger-sqli/lab11-36.png)

En esta pestaña seleccionaremos el **Payload set: 1**, **Payload type: numbers** y abajo seleccionamos **From: 1**, **To: 20** y **Step: 1** para indicar que queremos ir del número 1 al 20 avanzando de 1 en 1.

![](/images/images-portswigger-sqli/lab11-37.png)

Luego seleccionaremos el segundo payload set y le indicaremos que queremos un **Payload type: Brute forcer**. Abajo indicaremos un **Min length: 1** y **Max length: 1**, esto significa que por cada petición cambiará el **a** que marcamos anteriormente por una letra del **Character set**.

![](/images/images-portswigger-sqli/lab11-38.png)

Hay que recordar que la contraseña puede contener mayúsculas también, así que agregaremos el abecedario en mayúsculas.

![](/images/images-portswigger-sqli/lab11-39.png)

Y hacemos click en el botón **Start attack** para iniciar el proceso de fuerza bruta.

![](/images/images-portswigger-sqli/lab11-40.png)

Cuando termine el proceso iremos a la pestaña **Options**.

![](/images/images-portswigger-sqli/lab11-41.png)

Buscamos **Grep - Match** y hacemos click en el botón **Clear**.

![](/images/images-portswigger-sqli/lab11-42.png)

Luego escribimos `Welcome back!` y hacemos click en el botón **Add**.

![](/images/images-portswigger-sqli/lab11-43.png)

Volvemos a la pestaña **Results** y hacemos click en la opción **Payload 1** hasta que quede con la flecha apuntando hacia arriba.

![](/images/images-portswigger-sqli/lab11-44.png)

Hacemos click en la opción **Welcome back!** hasta que quede con la flecha apuntado hacia abajo.

![](/images/images-portswigger-sqli/lab11-46.png)

Y así obtenemos la contraseña de administrador de forma ordenada.

![](/images/images-portswigger-sqli/lab11-47.png)

Volvemos a la página del reto y vamos a **My account**.

![](/images/images-portswigger-sqli/lab11-48.png)

Ingresamos la contraseña.

![](/images/images-portswigger-sqli/lab11-49.png)

Y resolvemos el laboratorio.

![](/images/images-portswigger-sqli/lab11-48.png)

---

## [Anterior](/sql-injection-attack-listing-the-database-contents-on-oracle)