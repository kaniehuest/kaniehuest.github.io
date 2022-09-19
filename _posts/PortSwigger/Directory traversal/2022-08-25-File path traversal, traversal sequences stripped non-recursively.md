---
title: PortSwigger - File path traversal, traversal sequences stripped non-recursively.
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto File path traversal, traversal sequences stripped non-recursively.
tags:
- portswigger
- directory-traversal
- post
- writeups
---
# Solución
---

Primera hacemos click derecho sobre una imágen y la abrimos en una pestaña nueva.

![](/assets/images/images-portswigger-dt/lab3-1.png)

![](/assets/images/images-portswigger-dt/lab3-2.png)

En Burpsuite vamos a la pestaña **Proxy** e interceptamos las peticiones haccienndo click en el botón **Intercept is off**, si se pone de color azul estará interceptando.

![](/assets/images/images-portswigger-dt/lab3-3.png)

![](/assets/images/images-portswigger-dt/lab3-4.png)

Vamos a la imagen y recargamos la página.

![](/assets/images/images-portswigger-dt/lab3-5.png)

Vemos que interceptamos la petición y la enviamos a la pestaaña **Repeater** presionando los botones `CTRL + R`.

![](/assets/images/images-portswigger-dt/lab3-6.png)

Vamos a la pestaña **Repeater** y reemplazamos el nombre de la imágen.

El filtro de la página solo borra dos puntos y una barra. Entonces, si escribimos `....//` la página borrará dos puntos y una barra dejando el payload así:`../`.

Nuestro payload final es: `....//....//....//etc/passwd`.

Lo pegamos y hacemos click en el botón **Send**.

![](/assets/images/images-portswigger-dt/lab3-7.png)

Vemos que en la respuesta está el `/etc/passwd`.

![](/assets/images/images-portswigger-dt/lab3-8.png)

Volvemos a la pestaña **Proxy**  y para dejar de interceptar el tráfico hacemos click en **Intercept is on**.

![](/assets/images/images-portswigger-dt/lab3-9.png)

![](/assets/images/images-portswigger-dt/lab3-10.png)

Volvemos a la página y resolvemos el laboratorio.

![](/assets/images/images-portswigger-dt/lab3-11.png)


---

## [Anterior](/blog/File-path-traversal%2C-traversal-sequences-blocked-with-absolute-path-bypass)
## [Siguiente](/blog/File-path-traversal%2C-traversal-sequences-stripped-with-superfluous-URL-decode)