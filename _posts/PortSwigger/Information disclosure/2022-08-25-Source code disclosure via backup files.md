---
title: PortSwigger - Source code disclosure via backup files (sin Burpsuite).
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Source code disclosure via backup files.
tags:
- portswigger
- information-disclosure
- post
- writeups
---
# Solución
---

Primero vamos al archivo `robots.txt` agregandolo en la url.

![](/images/images-portswigger-id/lab3-1.png)

Cuando accedemos vemos un archivo `/backup` al que podemos acceder.

![](/images/images-portswigger-id/lab3-2.png)

Cuando vamos al archivo **backup** observamos un archivo `.bak`.

![](/images/images-portswigger-id/lab3-3.png)

La hacemos click.

![](/images/images-portswigger-id/lab3-4.png)

Vemos el contenido de un archivo.

![](/images/images-portswigger-id/lab3-5.png)

Si revisamos bien vemos que se realiza una conexión hacia una base de datos postgresql y se observa la contraseña.

![](/images/images-portswigger-id/lab3-6.png)

Volvemos al inicio y hacemos click en el botón **Submit solution**.

![](/images/images-portswigger-id/lab3-7.png)

Ingresamos la contraseña.

![](/images/images-portswigger-id/lab3-8.png)

Y resolvemos el laboratorio.

![](/images/images-portswigger-id/lab3-9.png)


---

## [Anterior](/information-disclosure-on-debug-page)
## [Siguiente](/authentication-bypass-via-information-disclosure)