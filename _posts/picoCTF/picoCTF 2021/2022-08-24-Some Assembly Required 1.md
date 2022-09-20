---
title: PicoCTF 2021 - Some Assembly Required 1
layout: post
post-image: /assets/images/gatohacker3.jpeg 
description: Resolución del reto Some Assembly Required 1. 
tags:
- picoctf
- ctf
- picoctf2021
- post
- writeups
---
# Solución
---

Como no hay descripción entonces vemos los archivos que tiene la página en las **herramientas de desarrollador** y luego en la pestaña **Debugger**.

Después nos vamos a la pestaña que dice **wasm://** y vemos que hay un archivo wasm dentro. Si no te muestra el archivo como a mí, debes recargar la página.

![](/images/images-picoctf-2021/sar-1.png)

Podemos ver un archivo wasm.

![](/images/images-picoctf-2021/sar-2.png)

Si vamos al final del archivo veremos la flag.

![](/images/images-picoctf-2021/sar-3.png)


# Flag
---

`picoCTF{8857462f9e30faae4d037e5e25fee1ce}`

---

## [Anterior](/Scavenger-Hunt)
## [Siguiente](/Who-are-you)