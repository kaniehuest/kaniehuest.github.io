---
title: PicoCTF 2022 - Roboto Sans
layout: post
post-image: /assets/images/gatohacker3.jpeg 
description: Resolución del reto Roboto Sans. 
tags:
- picoctf
- ctf
- picoctf2022
- post
- writeups
---
# Descripción
---

The flag is somewhere on this web application not necessarily on the website. Find it.


# Solución
---

La página principal no nos muestra nada interesante, pero como el reto se llama roboto seguramente encontraremos algo en el archivo **robots.txt**.

![](/assets/images/images-picoctf-2022/roboto-sans-1.png)

Encontramos unas cadenas de texto codificadas en base64.

![](/assets/images/images-picoctf-2022/roboto-sans-2.png)

Si decodificamos la segunda línea podemos ver un archivo.

![](/assets/images/images-picoctf-2022/roboto-sans-3.png)

Si vamos a ese archivo en la página web podemos ver la flag.

![](/assets/images/images-picoctf-2022/roboto-sans-4.png)


# Flag
---

`picoCTF{Who_D03sN7_L1k5_90B0T5_22ce1f22}`

---

## [Anterior](/blog/Power-Cookie)
## [Siguiente](/blog/Secrets)