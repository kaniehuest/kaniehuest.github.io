---
title: PortSwigger - Information disclosure in error messages (sin Burpsuite).
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Information disclosure in error messages.
tags:
- portswigger
- information-disclosure
- post
- writeups
---
# Solución
---

Primero hacemos click en **View details**.

![](/images/images-portswigger-id/lab1-1.png)

Vemos que el id en la url es un número.

![](/images/images-portswigger-id/lab1-2.png)

Lo ponemos entre comillas esperando que el servidor lo interprete como una string y falle.

![](/images/images-portswigger-id/lab1-3.png)

Lo enviamos y efectivamente el servidor lo interpreta como string y falla.

![](/images/images-portswigger-id/lab1-4.png)

Vemos al final la versión de Apache que necesitamos para terminar el laboratorio.

![](/images/images-portswigger-id/lab1-5.png)

Volvemos a la página principal del laboratorio y hacemos click en **Submit solution**.

![](/images/images-portswigger-id/lab1-6.png)

Ingresamos nuestra respuesta y hacemos click en **OK**.

![](/images/images-portswigger-id/lab1-7.png)

Y resolvemos el laboratorio.

![](/images/images-portswigger-id/lab1-8.png)


---

## [Siguiente](/information-disclosure-on-debug-page)