---
title: PicoCTF 2019 - Irish-Name-Repo 2 
layout: post
post-image: /assets/images/gatohacker3.jpeg 
description: Resolución del reto Irish-Name-Repo 2 
tags:
- picoctf
- ctf
- picoctf2019
- post
- writeups
---
# Descripción
---

There is a website running at  _Link_. Someone has bypassed the login before, and now it's being strengthened. Try to see if you can still login!


# Hints
---

The password is being filtered.


# Solución
---

En la página principal hacemos click en **Admin Login**.

![](/assets/images/images-picoctf-2019/irish-name-repo-2-1.png)

El hint nos dice que el login es el mismo que en **Irish-Name-Repo 1**, solo que esta vez el campo de **Password** está securizado. Pero no dice nada del campo de **Username**, así que colocamos un payload simple de SQLI `admin' -- -`.

![](/assets/images/images-picoctf-2019/irish-name-repo-2-2.png)

Y podemos ver la flag.

![](/assets/images/images-picoctf-2019/irish-name-repo-2-3.png)


# Flag
---

`picoCTF{m0R3_SQL_plz_aee925db}`

---

## [Anterior](/blog/Irish-Name-Repo-1)
## [Siguiente](/blog/Irish-Name-Repo-3)