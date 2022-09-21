---
title: PortSwigger - File path traversal, traversal sequences stripped with superfluous URL-decode.
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto File path traversal, traversal sequences stripped with superfluous URL-decode.
tags:
- portswigger
- directory-traversal
- post
- writeups
---
# Solución
---

Primero hacemos click derecho sobre una imágen y la abrimos en una pestaña nueva.

![](/images/images-portswigger-dt/lab4-1.png)

![](/images/images-portswigger-dt/lab4-2.png)

Luego interceptamos las peticiones en Burpsuite haciendo click en el botón **Intercept is off** para que cambie a color azul.

![](/images/images-portswigger-dt/lab4-3.png)

![](/images/images-portswigger-dt/lab4-4.png)

Luego vamos a la pestaña del navegador donde está la imágen y recargamos la página.

![](/images/images-portswigger-dt/lab4-5.png)

Vemos que interceptamos la petición y la enviamos a la pestaña **Repeater** presionando los botones `CTRL + r`.

![](/images/images-portswigger-dt/lab4-6.png)

Cambiamos el nombre de la imágen por nuestro payload `..%252F..%252F..%252Fetc/passwd` y enviamos la petición.  

![](/images/images-portswigger-dt/lab4-7.png)

Vemos el archivo en pestaña **Response**.

![](/images/images-portswigger-dt/lab4-8.png)

Volvemos a la pestaña **Proxy** en Burpsuite y hacemos click en el botón **Intercept is on** para dejar de interceptar las peticiones.

![](/images/images-portswigger-dt/lab4-9.png)

![](/images/images-portswigger-dt/lab4-10.png)

Volvemos al navegador y resolvemos el laboratorio.

![](/images/images-portswigger-dt/lab4-11.png)



---

## [Anterior](/file-path-traversal-traversal-sequences-stripped-non-recursively)
## [Siguiente](/file-path-traversal-validation-of-start-of-path)