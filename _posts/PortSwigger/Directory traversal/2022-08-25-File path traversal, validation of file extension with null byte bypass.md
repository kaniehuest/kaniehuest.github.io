---
title: PortSwigger - File path traversal, validation of file extension with null byte bypass.
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto File path traversal, validation of file extension with null byte bypass.
tags:
- portswigger
- directory-traversal
- post
- writeups
---
# Solución
---

Hacemos click derecho sobre una imagen y la abrimos en una pestaña nueva.

![](/images/images-portswigger-dt/lab6-1.png)

![](/images/images-portswigger-dt/lab6-2.png)

Luego vamos a Burpsuite e interceptamos las peticiones haciendo click en el botón **Intercept is off** para que se ponga de color azul.

![](/images/images-portswigger-dt/lab6-3.png)

![](/images/images-portswigger-dt/lab6-4.png)

Ahora vamos a la pestaña en el navegador donde está la foto y recargamos.

![](/images/images-portswigger-dt/lab6-5.png)

Vemos que interceptamos la petición y la enviamos a la pestaña **Repeater** haciendo click derecho y **Send to repeater** o presionando los botones `CTRL + r`.

![](/images/images-portswigger-dt/lab6-6.png)

Vamos a la pestaña **Repeater** y modificamos el valor de `filename` por `../../../etc/passwd%00.png`.

![](/images/images-portswigger-dt/lab6-7.png)

Vemos el contenido del archivo en la pestaña **Response**.

![](/images/images-portswigger-dt/lab6-8.png)

Volvemos a la pestaña **Proxy** y hacemos click en el botón **Intercept is on** para dejar de interceptar las peticiones.

![](/images/images-portswigger-dt/lab6-9.png)

![](/images/images-portswigger-dt/lab6-10.png)

Volvemos al navegador y resolvemos el laboratorio.

![](/images/images-portswigger-dt/lab6-11.png)


---

## [Anterior](/file-path-traversal-validation-of-start-of-path)