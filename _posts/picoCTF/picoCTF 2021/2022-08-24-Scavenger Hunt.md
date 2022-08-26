---
title: PicoCTF 2021 - Scavenger Hunt
layout: post
post-image: /assets/images/gatohacker3.jpeg 
description: Resolución del reto Scavenger Hunt. 
tags:
- picoctf
- ctf
- picoctf2021
- post
- writeups
---
# Descripción
---

There is some interesting information hidden around this site. Can you find it?


# Hints
---

You should have enough hints to find the files, don't run a brute forcer.


# Solución
---

La descripción nos dice que hay información escondida en la aplicación, entonces hacemos click derecho y vemos el código fuente de la página principal. Ahí veremos la primera parte de la flag `picoCTF{t`.

![](/assets/images/images-picoctf-2021/scavenger-hunt-1.png)

Después damos un vistazo a los archivos **.css** y **.js** en busca de más pistas.

![](/assets/images/images-picoctf-2021/scavenger-hunt-2.png)

El archivo .css nos da la segunda parte de la flag `h4ts_4_l0`.

![](/assets/images/images-picoctf-2021/scavenger-hunt-3.png)

Si vamos al archivo .js veremos que nos hace una pregunta. Si googleas encontrarás que la respuesta es el archivo **robots.txt**.

![](/assets/images/images-picoctf-2021/scavenger-hunt-4.png)


Si vamos al archivo veremos la tercera parte de la flag `t_0f_pl4c` y una pregunta. La respuesta a la pregunta es el archivo **.htaccess**.

![](/assets/images/images-picoctf-2021/scavenger-hunt-5.png)

Si vamos al archivo .htaccess veremos la cuarta parte de la flag `3s_2_lO0k` y otra pregunta. La respuesta es el archivo **.DS_Store**.

![](/assets/images/images-picoctf-2021/scavenger-hunt-6.png)

Si vamos al archivo veremos la última parte de la flag `_f7ce8828}`.

![](/assets/images/images-picoctf-2021/scavenger-hunt-7.png)


## Respuesta a las preguntas

Saber googlear una pregunta es una habilidad aparte, acá te muestra qué busqueda hice para encontrar las respuesta.


**Pregunta:**
- How can I keep Google from indexing my website?

**Respuesta:**

Pracamente copiamos y pegamos la pregunta en google y vemos una pregunta en **Stack Overflow**.

![](/assets/images/images-picoctf-2021/scavenger-hunt-8.png)

![](/assets/images/images-picoctf-2021/scavenger-hunt-10.png)

Vemos que en esta pregunta de **Stack Overflow** se hace mención al archivo robots.txt.


**Pregunta:**

- I think this is an apache server... can you Access the next flag?

**Respuesta:**

Podemos ver que la palabra Access está en mayúscula así que deberíamos agregar esa palabra a nuestra búsqueda.

![](/assets/images/images-picoctf-2021/scavenger-hunt-9.png)

Vemos que en 6 occaciones se hace mención al archivo .htaccess. 


**Pregunta:**

- I love making websites on my Mac, I can Store a lot of information there.

**Respuesta:**

Las palabras en mayúsculas nos dan una pista de cómo debemos hacer nuestra búsqueda. Si buscamos un archivo de un sitio web y le agregamos estas palabras claves podemos encontrar la respuesta en la primera página.

![](/assets/images/images-picoctf-2021/scavenger-hunt-11.png)


# Flag
---

`picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_f7ce8828}`

---

## [Anterior](/blog/Cookies)
## [Siguiente](/blog/Some-Assembly-Required-1)