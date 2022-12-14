---
title: PicoCTF 2019 - Irish-Name-Repo 3 
layout: post
post-image: /assets/images/gatohacker3.jpeg 
description: Resolución del reto Irish-Name-Repo 3 
tags:
- picoctf
- ctf
- picoctf2019
- post
- writeups
---
# Descripción
---

There is a secure website running at  _Link_. Try to see if you can login as admin!


# Hints
---

Seems like the password is encrypted.


# Solución
---

En la página principal hacemos click en el botón **Admin Login**.

![](/images/images-picoctf-2019/irish-name-repo-3-1.png)

No tenemos ninguna pista útil, así que miramos el código fuente de la página haciendo click derecho y en **Inspeccionar**.

![](/images/images-picoctf-2019/irish-name-repo-3-2.png)

Luego seleccionamos la parte de **body** del cógido HTML, hacemos click derecho y seleccionamos **Expandir de manera recurrente** para poder ver todo el código fuente.

![](/images/images-picoctf-2019/irish-name-repo-3-3.png)

Notamos un **Input** que es de tipo **hidden** y tiene como nombre **debug**.

![](/images/images-picoctf-2019/irish-name-repo-3-4.png)

Para hacerlo visible simplemente eliminamos el texto **hidden**.

![](/images/images-picoctf-2019/irish-name-repo-3-5.png)

Recargamos la página y vemos un nuevo input con el número 0. 

![](/images/images-picoctf-2019/irish-name-repo-3-6.png)

Si escribimos nuestro payload de SQLi `' or 1=1-- -`, cambiamos el 0 a un 1 y hacemos click en login veremos información extra sobre la petición.

![](/images/images-picoctf-2019/irish-name-repo-3-8.png)

Podemos ver cómo se ejecuta la query en el servidor. Vemos que transforma nuestro `or` a `be`.

![](/images/images-picoctf-2019/irish-name-repo-3-7.png)

Si escribimos todo el abecedario nos damos cuenta que las letras están desfasadas un número de espacios.

Si escribimos `abcdefghijklmnopqrstuvwxyz`, el servidor lo trasforma a `nopqrstuvwxyzabcdefghijklm`, por lo tanto, podemos notar que es rot13.

![](/images/images-picoctf-2019/irish-name-repo-3-9.png)

Para combrobarlo vamos a [CyberChef](https://gchq.github.io/CyberChef/), y en el campo de **Input** escribimos `or`.

![](/images/images-picoctf-2019/irish-name-repo-3-10.png)

Después escribimos `rot13` en **Operations** y arrastramos ROT13 a **Recipe**.

![](/images/images-picoctf-2019/irish-name-repo-3-11.png)

Comprobamos que es rot13 porque anteriormente escribimos **or** y el servidor nos mostraba **be**.

![](/images/images-picoctf-2019/irish-name-repo-3-12.png)

Y si ahora escribimos **be** podemos ver que nos devuelve **or**.

![](/images/images-picoctf-2019/irish-name-repo-3-13.png)

Con esto en mente, nuestro payload quedaría así: 
`' be 1=1 -- -`

![](/images/images-picoctf-2019/irish-name-repo-3-14.png)

Y podemos iniciar sesión.

![](/images/images-picoctf-2019/irish-name-repo-3-15.png)


# Flag
---

`picoCTF{3v3n_m0r3_SQL_7f5767f6}`


---

## [Anterior](/irish-name-repo-2)
## [Siguiente](/jawt-scratchpad)