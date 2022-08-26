---
title: CTFlearn - POST Practice
layout: post
post-image: /assets/images/gatohacker2.jpeg 
description: La resolución del reto POST Practice.
tags:
- ctflearn
- post
- writeups
---
# Descripción
---

This website requires authentication, via POST. However, it seems as if someone has defaced our site. Maybe there is still some way to authenticate? 


# Solución
---

En la página principal nos indica que debemos realizar una petición por el método POST, con información que aún no obtenemos.

![](/assets/images/images-ctflearn/post-p-1.png)

Si apretamos `CTRL + u`  podemos ver el código fuente de la página, y nos muestra credenciales.

![](/assets/images/images-ctflearn/post-p-2.png)

En mi caso usaré la terminal y el comando **curl** para resolver el reto.

Primero realizamos una petición por el método POST con el siguiente comando:

```bash
$ curl  -X POST http://165.227.106.113/post.php 
```

![](/assets/images/images-ctflearn/post-p-3.png)

Con las credenciales obtenidas, solo nos falta construir el comando para realizar la petición.

Con este comando indicamos que queremos realizar una petición con el método post y que queremos agregar una cabezera para poder enviar data, después agregamos nuestra data y obtenemos la flag.

```bash
$ curl -X POST http://165.227.106.113/post.php -d 'username=admin&password=71urlkufpsdnlkadsf' -H 'Content-Type: application/x-www-form-urlencoded'
```

![](/assets/images/images-ctflearn/post-p-4.png)


# Flag
---

`flag{p0st_d4t4_4ll_d4y}`