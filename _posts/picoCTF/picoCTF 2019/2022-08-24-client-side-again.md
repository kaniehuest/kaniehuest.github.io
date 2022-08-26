---
title: PicoCTF 2019 - Client-side-again 
layout: post
post-image: /assets/images/gatohacker3.jpeg 
description: Resolución del reto client-side-again.
tags:
- picoctf
- ctf
- picoctf2019
- post
- writeups
---
# Descripción
---

Can you break into this super secure portal? 


# Hints
---

What is obfuscation?


# Solución
---

Hacemos click derecho y seleccionamos **Inspeccionar**.

![](/assets/images/images-picoctf-2019/client-side-again-1.png)

Luego nos vamos a la pestaña **Sources**.

![](/assets/images/images-picoctf-2019/client-side-again-2.png)

Si no nos aparece nada debemos recargar la página.

![](/assets/images/images-picoctf-2019/client-side-again-3.png)

Se ve que está ofuscado, por lo tanto hacemos click en **Pretty print**.

![](/assets/images/images-picoctf-2019/client-side-again-4.png)

Y podemos notar un array con la flag dividida en distintas partes.

![](/assets/images/images-picoctf-2019/client-side-again-5.png)

# Flag
---

`picoCTF{not_this_again_337115}`

---

## [Anterior](/blog/picobrowser)
## [Siguiente](/blog/Irish-Name-Repo-1)