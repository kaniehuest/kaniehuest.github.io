---
title: PortSwigger - File path traversal, validation of start of path.
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto File path traversal, validation of start of path.
tags:
- portswigger
- directory-traversal
- post
- writeups
---
# Solución
---

Primero hacemos click derecho sobre una imagen y la abrimos en una pestaña nueva.

![](/assets/images/images-portswigger-dt/lab5-1.png)

![](/assets/images/images-portswigger-dt/lab5-2.png)

Luego vamos a Burpsuite y hacemos clikc en el botón **Intercept is off** para interceptar las peticiones.

![](/assets/images/images-portswigger-dt/lab5-3.png)

![](/assets/images/images-portswigger-dt/lab5-4.png)

Vamos a la página donde está la foto y recargamos.

![](/assets/images/images-portswigger-dt/lab5-5.png)

Interceptamos la petición y la enviamos a la pestaña **Repeater** presionando las teclas `CTRL + r`.

![](/assets/images/images-portswigger-dt/lab5-6.png)

En la pestaña repeater cambiamos la ruta de la imagen por `/var/www/images/../../../etc/passwd` y hacemos click en el botón **Send**.

![](/assets/images/images-portswigger-dt/lab5-7.png)

Vemos en la pestaña **Response** el contendio del archivo `/etc/passwd`.

![](/assets/images/images-portswigger-dt/lab5-8.png)

Volvemos a la pestaña **Proxy** y hacemos click en el botón **Intercept is on** para dejar de interceptar las peticiones.

![](/assets/images/images-portswigger-dt/lab5-9.png)

![](/assets/images/images-portswigger-dt/lab5-10.png)

Volvemos al navegador y resolvemos el laboratorio.

![](/assets/images/images-portswigger-dt/lab5-11.png)
