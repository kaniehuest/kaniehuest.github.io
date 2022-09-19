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

![](/assets/images/images-portswigger-id/lab3-1.png)

Cuando accedemos vemos un archivo `/backup` al que podemos acceder.

![](/assets/images/images-portswigger-id/lab3-2.png)

Cuando vamos al archivo **backup** observamos un archivo `.bak`.

![](/assets/images/images-portswigger-id/lab3-3.png)

La hacemos click.

![](/assets/images/images-portswigger-id/lab3-4.png)

Vemos el contenido de un archivo.

![](/assets/images/images-portswigger-id/lab3-5.png)

Si revisamos bien vemos que se realiza una conexión hacia una base de datos postgresql y se observa la contraseña.

![](/assets/images/images-portswigger-id/lab3-6.png)

Volvemos al inicio y hacemos click en el botón **Submit solution**.

![](/assets/images/images-portswigger-id/lab3-7.png)

Ingresamos la contraseña.

![](/assets/images/images-portswigger-id/lab3-8.png)

Y resolvemos el laboratorio.

![](/assets/images/images-portswigger-id/lab3-9.png)


---

## [Anterior](/blog/Information-disclosure-on-debug-page)
## [Siguiente](/blog/Authentication-bypass-via-information-disclosure)