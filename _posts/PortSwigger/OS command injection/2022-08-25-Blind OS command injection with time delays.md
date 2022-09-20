---
title: PortSwigger - Blind OS command injection with time delays (sin Burpsuite).
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Blind OS command injection with time delays.
tags:
- portswigger
- os-command-injection
- post
- writeups
---
# Solución
---

Navegador: **Firefox**

Primero hacemos click en el botón **Submit feedback**.

![](/images/images-portswigger-osci/lab2-1.png)

Abrimos las herramientas de desarrollador y vamos a la pestaña **Network**.

![](/images/images-portswigger-osci/lab2-2.png)

Rellenamos el formulario y hacemos click en el botón **Submit feedback**.

![](/images/images-portswigger-osci/lab2-3.png)

Vemos que se realiza una petición por el método POST que editaremos haciendo click derecho y en **Edit and Resend**.

![](/images/images-portswigger-osci/lab2-4.png)

Vemos que se abre una ventana la derecha con el nombre **New Request**.

![](/images/images-portswigger-osci/lab2-5.png)

Después de nuestro email inyectamos nuestro comando `||sleep 10||`.

![](/images/images-portswigger-osci/lab2-6.png)

Luego hacemos click en el botón **Send**.

![](/images/images-portswigger-osci/lab2-7.png)

Vemos que nuestra petición se realizó correctamente, podemos comprobarlo haciendole click a la petición y yendo a la pestaña **Timings** vemos que se demoró 10 segundos.

![](/images/images-portswigger-osci/lab2-8.png)

Y resolvemos el laboratorio sin el uso de Burpsuite.

![](/images/images-portswigger-osci/lab2-9.png)


---

## [Anterior](/OS-command-injection%2C-simple-case)
## [Siguiente](/Blind-OS-command-injection-with-output-redirection)