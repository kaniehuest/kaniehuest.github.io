---
title: PortSwigger - File path traversal, traversal sequences blocked with absolute path bypass.
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto File path traversal, traversal sequences blocked with absolute path bypass.
tags:
- portswigger
- directory-traversal
- post
- writeups
---
# Solución
---

Primero haces click derecho sobre una imágen y luego la abres en una pestaña nueva.

![](/assets/images/images-portswigger-dt/lab2-1.png)

Puedes notar un parámetro que necesita como valor el nombre de un archivo.

![](/assets/images/images-portswigger-dt/lab2-2.png)

Te vas a Burpsuite y haces click en **Intercept is off** para empezar a interceptar la petición.

![](/assets/images/images-portswigger-dt/lab2-3.png)

![](/assets/images/images-portswigger-dt/lab2-4.png)

Luego te vas al navegador y recargas la página.

![](/assets/images/images-portswigger-dt/lab2-5.png)

Interceptas la petción y la envías a la pestaña **Repeater** presionando las teclas `CTRL + R`.

![](/assets/images/images-portswigger-dt/lab2-6.png)

En la pestaña **Repeater** modificas el valor del parámetro por `/etc/passwd` y apretas el botón **Send**.

![](/assets/images/images-portswigger-dt/lab2-7.png)

Y puedes ver la respuesta de la petción a la derecha que muestra el contenido del `/etc/passwd`.

![](/assets/images/images-portswigger-dt/lab2-8.png)

Dejas de interceptar la petición en la pestaña **Proxy** haciendo click en el botón **Intercept is on**.

![](/assets/images/images-portswigger-dt/lab2-9.png)

![](/assets/images/images-portswigger-dt/lab2-10.png)

Vuelves al navegador y terminas el laboratorio.

![](/assets/images/images-portswigger-dt/lab2-11.png)


---

## [Anterior](/blog/File-path-traversal%2C-simple-case)
## [Siguiente](/blog/File-path-traversal%2C-traversal-sequences-stripped-non-recursively)