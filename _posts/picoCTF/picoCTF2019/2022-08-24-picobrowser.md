---
title: PicoCTF 2019 - picobrowser 
layout: post
post-image: /assets/images/gatohacker3.jpeg 
description: Resolución del reto picobrowser. 
tags:
- picoctf
- ctf
- picoctf2019
- post
- writeups
---
# Descripción
---

This website can be rendered only by picobrowser, go and catch the flag! 


# Hints
---

You don't need to download a new web browser


# Solución
---

Primero debemos irnos a la página donde está la flag haciendo click en el link.

![](/images/images-picoctf-2019/picobrowser-1.png)

Pero al entrar en la página nos dice que nuestro navegador no es **picobrowser**, como nos especificaron en la descripción, para visualizar la flag nuestro navegador debe ser picobrowser.

![](/images/images-picoctf-2019/picobrowser-2.png)

Para decirle a la página que nuestro navegador en **picobrowser** debemos ir a **Inspeccionar**.

![](/images/images-picoctf-2019/picobrowser-3.png)

Luego en irnos a la pestaña **Network**.

![](/images/images-picoctf-2019/picobrowser-4.png)

Y hacer click en el botón con símbolo de WIFI.

![](/images/images-picoctf-2019/picobrowser-5.png)

Nos aparecerá una pestaña más abajo donde debemos deshabilitar la opción **Use browser default**.

![](/images/images-picoctf-2019/picobrowser-6.png)

Y rellenar el campo vació con el nombre del navegador que queremos suplantar.

![](/images/images-picoctf-2019/picobrowser-7.png)

Si recargamos la página podemos ver la flag.

![](/images/images-picoctf-2019/picobrowser-8.png)


# Flag
---

`picoCTF{p1c0_s3cr3t_ag3nt_e9b160d0}`

---

## [Anterior](/dont-use-client-side)
## [Siguiente](/client-side-again)