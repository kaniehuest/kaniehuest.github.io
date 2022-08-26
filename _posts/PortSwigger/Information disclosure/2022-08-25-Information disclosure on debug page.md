---
title: PortSwigger - Information disclosure on debug page.
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Information disclosure on debug page.
tags:
- portswigger
- information-disclosure
- post
- writeups
---
# Solución
---

Primero abrimos el código fuente de la página en otra pestaña presionando `CTRL + u`.

![](/assets/images/images-portswigger-id/lab2-1.png)

Vemos el código fuente y buscamos algo raro.

![](/assets/images/images-portswigger-id/lab2-2.png)

Al final de la página vemos un comentario con la dirección de un archivo php.

![](/assets/images/images-portswigger-id/lab2-3.png)

Pegamos la dirección en la url y vamos al archivo.

![](/assets/images/images-portswigger-id/lab2-4.png)

Como el archivo es muy largo presionamos `CTRL + f` y escribimos `SECRET_KEY` porque es lo que necesitamos para resolver el laboratorio.

![](/assets/images/images-portswigger-id/lab2-5.png)

Volvemos a la página principal y hacemos click en el botón **Submit solution**.

![](/assets/images/images-portswigger-id/lab2-6.png)

Pegamos el valor del **SECRET_KEY** y hacemos click en el botón **OK**.

![](/assets/images/images-portswigger-id/lab2-7.png)

Y resolvemos el laboratorio.

![](/assets/images/images-portswigger-id/lab2-8.png)