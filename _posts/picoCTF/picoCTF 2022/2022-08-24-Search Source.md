---
title: PicoCTF 2022 - Search Source
layout: post
post-image: /assets/images/gatohacker3.jpeg 
description: Resolución del reto Search Source. 
tags:
- picoctf
- ctf
- picoctf2022
- post
- writeups
---
# Descripción
---

The developer of this website mistakenly left an important artifact in the website source, can you find it?


# Hints
---

- How could you mirror the website on your local machine so you could use more powerful tools for searching?


# Solución
---

Primero debes abrir las herramientos de desarollador.

![](/images/images-picoctf-2022/search-source-1.png)

Luego te vas a la pestaña **Style Editor** y buscas el archivo **style.css**.

![](/images/images-picoctf-2022/search-source-2.png)

Apretas `CTRL + f` y escribes `pico` para buscar la palabra pico por todo el archivo y encontrarás la flag.

![](/images/images-picoctf-2022/search-source-3.png)


# Flag
---

`picoCTF{1nsp3ti0n_0f_w3bpag3s_ec95fa49}`

---

## [Anterior](/Local-Authority)
## [Siguiente](/Forbidden-Paths)