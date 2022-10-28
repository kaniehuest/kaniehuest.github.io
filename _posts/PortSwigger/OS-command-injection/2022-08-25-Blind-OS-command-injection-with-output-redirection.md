---
title: PortSwigger - Blind OS command injection with output redirection (sin Burpsuite).
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Blind OS command injection with output redirection.
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

![](/images/images-portswigger-osci/lab3-1.png)

Abrimos las herramientas de desarrollador y vamos a la pestaña **Network**.

![](/images/images-portswigger-osci/lab3-2.png)

Rellenamos el formulario y hacemos click en **Submit feedback**.

![](/images/images-portswigger-osci/lab3-3.png)

Vemos que se realiza una petición con el método POST que podemos editar haciendo click derecho y en **Edit and Resend**.

![](/images/images-portswigger-osci/lab3-4.png)

Observamos una nueva pestaña a la derecha llamada **New Request**.

![](/images/images-portswigger-osci/lab3-5.png)

Inyectamos nuestro payload al final de nuestro correo electrónico `||whoami > hola.txt||`. Este payload ejecuta el comando **whoami** y redirige el output a un archivo que llamaremos **hola.txt**.

![](/images/images-portswigger-osci/lab3-6.png)

Hacemos click en el botón **Send**.

![](/images/images-portswigger-osci/lab3-7.png)

Vemos que nuestra petición tiene de estado el número 200, por lo tanto todo se realizó correctamente.

![](/images/images-portswigger-osci/lab3-8.png)

Volvemos a la página principal del reto y abrimos una imagen en una pestaña nueva.

![](/images/images-portswigger-osci/lab3-9.png)

Nos fijamos que en la url se está entregando el nombre de un archivo, así que, en lugar de **65.jpg** escribiremos el nombre del archivo en el que escribimos el output del comando.

![](/images/images-portswigger-osci/lab3-10.png)
Yo le puse **hola.txt** al archivo, por lo tanto escribiré hola.txt y vemos el resultado del comando **whoami**.

![](/images/images-portswigger-osci/lab3-11.png)

Y resolvemos el laboratorio sin necesidad de Burpsuite.

![](/images/images-portswigger-osci/lab3-12.png)


---

## [Anterior](/blind-os-command-injection-with-time-delays)