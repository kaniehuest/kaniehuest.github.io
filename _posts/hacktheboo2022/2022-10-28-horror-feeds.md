---
title: Hack The Boo 2022 - Horror Feeds
layout: post
description: La resolución del reto "Horror Feeds" del CTF "Hack The Boo 2022" organizado por Hack The Box.
tags:
- HackTheBox
- HorrorFeeds
- HackTheBoo
- ctf
- post
- writeups
---
# Descripción
---

An unknown entity has taken over every screen worldwide and is broadcasting this haunted feed that introduces paranormal activity to random internet-accessible CCTV devices. Could you take down this streaming service?

# Solución
---

El tercer reto web del CTF nos presenta un panel de inicio de sesión. 

![](/images/images-hacktheboo2022/hf-1.png)

Podemos registrarnos.

![](/images/images-hacktheboo2022/hf-2.png)

Al iniciar sesión podemos ver unas cámaras de una oficina donde ocurren eventos paranormales xd, no hay nada más que hacer, solo un botón para cerrar sesión.

![](/images/images-hacktheboo2022/hf-3.png)

Si abrimos las herramientas de desarrollador podemos observar un JWT.

![](/images/images-hacktheboo2022/hf-4.png)

Pegamos el valor en la página [jwt.io](https://jwt.io/), pero no observamos nada importante.

![](/images/images-hacktheboo2022/hf-5.png)

Leyendo el código fuente encontramos la función `dashboard()`, esta función renderiza la plantilla `dashboard.html` y pasa lo que parece la flag y el nombre de usuario.

![](/images/images-hacktheboo2022/hf-6.png)

La valor de la flag se encuentra en `current_app.config['FLAG']`, si vamos al archivo `config.py` podemos confirmar que la variable `FLAG` abre el archivo flag.txt y guarda su valor. Ahora que sabemos que la flag se renderiza en la misma página que las pantallas debemos encontrar una forma de verla.

![](/images/images-hacktheboo2022/hf-7.png)

Buscamos en `dashboard.html` el lugar donde se renderize la flag, pero nos muestra que se renderiza en una tabla y nosotros no vimos ninguna tabla anteriormente.

![](/images/images-hacktheboo2022/hf-8.png)

Vemos que se produce una comparación, si nuestro nombre de usuario es **admin** entonces podemos ver una tabla donde se encontrará la flag.

![](/images/images-hacktheboo2022/hf-9.png)

En el archivo `entrypoint.sh` se observa un script donde se crea una tabla de usuarios junto a un usuario **admin**, esto significa que no podremos simplemente crear una cuenta de administrador.

![](/images/images-hacktheboo2022/hf-10.png)

Podemos hacer fuerza bruta al login, colocar la contraseña que se ve más abajo o intentar romper el hash pero ya adelanto que no pasa nada.

![](/images/images-hacktheboo2022/hf-11.png)

Leyendo con más atención el código vemos que una query a diferencia de las otras ingresa las variables directamente, esto hace que la query **INSERT** sea vulnerable a SQLI.

![](/images/images-hacktheboo2022/hf-12.png)

Explotar una SQLI puede llevar muchos intentos, por esta razón ejecuté el archivo `build-docker.sh` que viene con el reto para tener la aplicación el local y que las querys se ejecuten más rápidamente, aparte de poder ver como se guardan mis querys en la base de datos.

![](/images/images-hacktheboo2022/hf-13.png)

Con la aplicación docker de escritorio me conecté a la base de datos con los datos que se ven en el archivo `entrypoint.sh`.

![](/images/images-hacktheboo2022/hf-14.png)

Primero intenté crear un usuarios para confirmar la vulnerabilidad.

```perl
usuarios1", "contrasña")-- -
```

![](/images/images-hacktheboo2022/hf-15.png)

Seleccionamos la tabla en el contenedor docker y confirmamos que el panel de registro es vulnerable a SQLi.

![](/images/images-hacktheboo2022/hf-16.png)

Creamos un usario con una contraseña fácil para obtener un hash válido, con el fin de cambiarle la contraseña al usuario admin y colocarle nuestro hash.

![](/images/images-hacktheboo2022/hf-17.png)

Mientras realizaba este reto se me ocurrió eliminar al usuario **admin** y crear uno nuevo :v, esto sería más rápido. Pero después de varios intentos fallidos me puse a leer el archivo `entrypoint.sh` y encontré la respuesta, solo tenemos permisos SELECT, INSERT y UPDATE. Curiosos que tengamos permiso de UPDATE si la aplicación solo utiliza el SELECT e INSERT jajajaaja. 

![](/images/images-hacktheboo2022/hf-18.png)

Creamos nuestra query y en el lugar de la password pegamos el hash que creamos anteriormente, yo creé un usuario con la contraseña `123` y esa será la contraseña del usuario **admin**.

```perl
usuario3", "contraseña"); UPDATE users SET password = "$2b$12$Y3iVqScZ/7jHuirW0nPaLuxLnGJVFLS55rW1RYuJ4nK/ukpaDwgI." WHERE username = "admin"-- -
```

![](/images/images-hacktheboo2022/hf-19.png)

Esta inyección no funcionaba y me tomó varias horas de intentos fallidos.

![](/images/images-hacktheboo2022/hf-20.png)

Googleando me encontré con la página de HackTricks donde existen varias formas de intentar explotar un SQLI por INSERT [Link de HackTricks](https://book.hacktricks.xyz/pentesting-web/sql-injection#insert-statement). Estuve leyendo y probando cada forma hasta que llegué a **ON DUPLICATE KEY UPDATE**, esto le dice al motor de base de datos qué hacer cuando una fila se repita, como nos dice HackTricks podemos utilizar esto para cambiar la contraseña del admin que es lo que estamos buscando.

Nuestra query final quedaría así:

```perl
usuario8", "contraseña"), ("admin", "contraseña") ON DUPLICATE KEY UPDATE password = "$2b$12$Y3iVqScZ/7jHuirW0nPaLuxLnGJVFLS55rW1RYuJ4nK/ukpaDwgI."-- -
```

![](/images/images-hacktheboo2022/hf-21.png)

Comprobamos en nuestra base de datos si se cambió el hash del usuario admin.

![](/images/images-hacktheboo2022/hf-22.png)

Ahora podemos iniciar sesión con el usuario admin y la contraseña 123.

![](/images/images-hacktheboo2022/hf-23.png)

Al iniciar sesión vemos las tablas y nuestra flag de prueba.

![](/images/images-hacktheboo2022/hf-24.png)

Copiamos y pegamos el payload que construimos en la aplicación real.

![](/images/images-hacktheboo2022/hf-25.png)

Deberiamos poder iniciar sesión como admin y la contraseña 123 también.

![](/images/images-hacktheboo2022/hf-26.png)

Bajamos un poco y obtenemos la flag del reto.

![](/images/images-hacktheboo2022/hf-27.png)

# Flag
---

`HTB{N3ST3D_QU3R1E5_AR3_5CARY!!!}`
