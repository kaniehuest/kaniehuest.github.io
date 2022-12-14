---
title: PortSwigger - Authentication bypass via information disclosure (sin Burpsuite).
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Authentication bypass via information disclosure.
tags:
- portswigger
- information-disclosure
- post
- writeups
---
# Solución
---

Navegador: **Firefox**

Primero hacemos click en el botón **My account**.

![](/images/images-portswigger-id/lab4-1.png)

Iniciamos sesión con las credenciales que nos indica la descripción del laboratorio.

![](/images/images-portswigger-id/lab4-2.png)

![](/images/images-portswigger-id/lab4-3.png)

Cuando iniciemos sesión iremos a la ruta `/admin`. Una vez que estemos ahí la página nos indica que solo los usuarios locales tienen permiso de usar las funciones de admin.

![](/images/images-portswigger-id/lab4-4.png)

Abrimos las herramientas de desarrollador.

![](/images/images-portswigger-id/lab4-5.png)

Y nos vamos a la pestaña **Network**.

![](/images/images-portswigger-id/lab4-6.png)

Recargando la página vemos una petición GET con el número de estado 401.

![](/images/images-portswigger-id/lab4-7.png)

Si le hacemos click derecho y luego seleccionamos la opción **Edit and Resend** nos aparecerá una pestaña a la derecha.

![](/images/images-portswigger-id/lab4-8.png)

Cambiamos el método de la petición por el **TRACE**.

![](/images/images-portswigger-id/lab4-9.png)

Y enviamos la petición haciendo click en el botón **Send**.

![](/images/images-portswigger-id/lab4-10.png)

Vemos que nuestra nueva petición tiene de esta el número 200.

![](/images/images-portswigger-id/lab4-11.png)

Le hacemos click a nuestra petición y nos vamos a la pestaña **Response**.

![](/images/images-portswigger-id/lab4-12.png)

Copiamos la cadena en base64 y la pegamos en cualquier decodificador de base64 en internet, yo utilizé Cyberchef.

![](/images/images-portswigger-id/lab4-13.png)

Notamos que se agrega una cabecera nueva a nuestra petición con nuestra dirección IP.

![](/images/images-portswigger-id/lab4-14.png)

Hacemos click derecho sobre nuestra petición anterior y luego seleccionamos la opción **Edit and Resend** nuevamente.

![](/images/images-portswigger-id/lab4-15.png)

En el campo **Request Headers** agregamos la cabecera que vimos anteriormente.

![](/images/images-portswigger-id/lab4-16.png)

Cambiamos nuestra IP por 127.0.0.1 para indicar que nuestra dirección IP es local.

![](/images/images-portswigger-id/lab4-17.png)

Cambiamos el método a GET.

![](/images/images-portswigger-id/lab4-18.png)

Y hacemos click en el botón **Send**.

![](/images/images-portswigger-id/lab4-19.png)

Nuestra petición tiene como estado el número 200.

![](/images/images-portswigger-id/lab4-20.png)

La seleccionamos y vamos a la pestaña **Response**.

![](/images/images-portswigger-id/lab4-21.png)

Bajamos y al final vemos 2 opcione, eliminar el usuario carlos y el usuario wiener.

![](/images/images-portswigger-id/lab4-22.png)

Si pasamos el cursor sobre la palabra **Delete** marcada en azul podemos ver un enlace `/admin/delete?username=carlos`.

![](/images/images-portswigger-id/lab4-23.png)

Agregamos esto a la URL y vemos que la página nuevamente nos pide la cabecera para indicar que somos usuarios locales.

![](/images/images-portswigger-id/lab4-24.png)

En las herramientas de desarrollador vemos la petición con número de estado 401.

![](/images/images-portswigger-id/lab4-25.png)

Le hacemos click derecho y seleccionamos la opción **Edit and Resend**.

![](/images/images-portswigger-id/lab4-26.png)

Agregamos la cabecera anterior.

![](/images/images-portswigger-id/lab4-27.png)

Seleccionamos el botón **Send**.

![](/images/images-portswigger-id/lab4-28.png)

Y resolvemos el laboratorio.

![](/images/images-portswigger-id/lab4-29.png)


---

## [Anterior](/source-code-disclosure-via-backup-files)
## [Siguiente](/information-disclosure-in-version-control-history)