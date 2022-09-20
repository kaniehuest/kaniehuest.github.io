---
title: PortSwigger - Username enumeration via different responses
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Username enumeration via different responses.
tags:
- portswigger
- authentication-vulnerabilities
- post
- writeups
---
# Solución
---

Primera hacemos click en el botón **My account**.

![](/images/images-portswigger-auth/lab1-1.png)

Ingresamos cualquier cosa en el panel de login.

![](/images/images-portswigger-auth/lab1-2.png)

Luego en Burpsuite hacemos click en **Intercept is off** para que quede en **Intercept is on**.

![](/images/images-portswigger-auth/lab1-3.png)

Debería quedar así

![](/images/images-portswigger-auth/lab1-4.png)

Después en la página web hacemos click en **Log in**.

![](/images/images-portswigger-auth/lab1-5.png)

Vemos que interceptamos la petición correctamente.

![](/images/images-portswigger-auth/lab1-6.png)

Enviamos la petición a la pestaña **Intruder** y hacemos click en el botón **Clear*.

![](/images/images-portswigger-auth/lab1-7.png)

Luego remarcamos la que pusimos en **username** y hacemos click en el botón **Add**.

![](/images/images-portswigger-auth/lab1-8.png)

Debería verse así:

![](/images/images-portswigger-auth/lab1-9.png)

Primero debemos copiar la [lista de usuarios](https://portswigger.net/web-security/authentication/auth-lab-usernames), luego vamos a la pestaña **Payloads** y hacemos click en el botón **Paste**.

![](/images/images-portswigger-auth/lab1-10.png)

Después hacemos click en el botón **Start attack**.

![](/images/images-portswigger-auth/lab1-11.png)

Esperamos un poco y vemos una petición que tiene un largo distinto al resto. Si inspeccionamos haciendo click vemos que el usuario está correcto pero la contraseña es incorrecta.

![](/images/images-portswigger-auth/lab1-12.png)

Volvemos a la pestaña **Positions** y hacemos click en el botón **Clear**.

![](/images/images-portswigger-auth/lab1-13.png)

Similar a lo anterior pero ahora seleccionamos el campo de **password** y luego en el botón **Add**.

![](/images/images-portswigger-auth/lab1-14.png)

Debemos cambiar el campo de usuario por el usuario que encontramos anteriormente y la petición debería verse así:

![](/images/images-portswigger-auth/lab1-15.png)

Volvemos a la pestaña **Payloads** y hacemos click en **Clear**.

![](/images/images-portswigger-auth/lab1-16.png)

Ahora copiamos el [listado de contraseñas](https://portswigger.net/web-security/authentication/auth-lab-passwords) que nos indica el laboratorio, hacemos click en **Paste** y finalmente hacemos click en **Start attack**.

![](/images/images-portswigger-auth/lab1-17.png)

Esperamos unos minutos y vemos una petición distinta a las otras, esta es la contraseña.

![](/images/images-portswigger-auth/lab1-18.png)

Recuerda dejar de interceptar las peticiones haciendo click en **Intercept is on**.

![](/images/images-portswigger-auth/lab1-20.png)

Debería quedar así.

![](/images/images-portswigger-auth/lab1-21.png)

Ingresa tus credenciales en el panel de login.

![](/images/images-portswigger-auth/lab1-19.png)

Y resolvemos el laboratorio.

![](/images/images-portswigger-auth/lab1-22.png)