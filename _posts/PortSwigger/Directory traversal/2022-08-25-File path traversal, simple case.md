---
title: PortSwigger - File path traversal, simple case.
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto File path traversal, simple case.
tags:
- portswigger
- directory-traversal
- post
- writeups
---
# Solución
---

Primero hacemos click derecho y abrimos la imagen en una nueva pestaña.

![](/assets/images/images-portswigger-dt/lab1-1.png)

Notamos en la url que se muestra un parametro que necesito un nombre de archivo.

![](/assets/images/images-portswigger-dt/lab1-2.png)

Si vamos a Burpsuite e interceptamos la petición.

![](/assets/images/images-portswigger-dt/lab1-3.png)

![](/assets/images/images-portswigger-dt/lab1-4.png)

Y recargamos la página.

![](/assets/images/images-portswigger-dt/lab1-5.png)

Vemos la peticón y la enviamos a la pestaña **Repeater** presionando `CTRL + R`.

![](/assets/images/images-portswigger-dt/lab1-6.png)

![](/assets/images/images-portswigger-dt/lab1-7.png)

Cuando estemos en la pestaña **Repeater** modificamos el valor del parámetro `filename` por `../../../etc/passwd` y hacemos click en el botón**Send**.

![](/assets/images/images-portswigger-dt/lab1-8.png)

Observamos en la pestaña **Response** el archivo **/etc/passwd**.

![](/assets/images/images-portswigger-dt/lab1-9.png)

Vamos de nuevo a la pestaña **Proxy** y hacemos click en **Intercept is on** para que quede en **Intercept is off** y así dejemos de interceptar la petición.

![](/assets/images/images-portswigger-dt/lab1-10.png)

Volvemos a la página y resolvemos el laboratorio.

![](/assets/images/images-portswigger-dt/lab1-11.png)