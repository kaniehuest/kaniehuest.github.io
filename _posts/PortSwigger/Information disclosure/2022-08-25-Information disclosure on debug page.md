---
title: PortSwigger - Information disclosure on debug page (sin Burpsuite).
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

![](/images/images-portswigger-id/lab2-1.png)

Vemos el código fuente y buscamos algo raro.

![](/images/images-portswigger-id/lab2-2.png)

Al final de la página vemos un comentario con la dirección de un archivo php.

![](/images/images-portswigger-id/lab2-3.png)

Pegamos la dirección en la url y vamos al archivo.

![](/images/images-portswigger-id/lab2-4.png)

Como el archivo es muy largo presionamos `CTRL + f` y escribimos `SECRET_KEY` porque es lo que necesitamos para resolver el laboratorio.

![](/images/images-portswigger-id/lab2-5.png)

Volvemos a la página principal y hacemos click en el botón **Submit solution**.

![](/images/images-portswigger-id/lab2-6.png)

Pegamos el valor del **SECRET_KEY** y hacemos click en el botón **OK**.

![](/images/images-portswigger-id/lab2-7.png)

Y resolvemos el laboratorio.

![](/images/images-portswigger-id/lab2-8.png)

---

## [Anterior](/information-disclosure-in-error-messages)
## [Siguiente](/source-code-disclosure-via-backup-files)