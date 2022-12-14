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

![](/images/images-picoctf-2021/scavenger-hunt-1.png)

Después damos un vistazo a los archivos **.css** y **.js** en busca de más pistas.

![](/images/images-picoctf-2021/scavenger-hunt-2.png)

El archivo .css nos da la segunda parte de la flag `h4ts_4_l0`.

![](/images/images-picoctf-2021/scavenger-hunt-3.png)

Si vamos al archivo .js veremos que nos hace una pregunta. Si googleas encontrarás que la respuesta es el archivo **robots.txt**.

![](/images/images-picoctf-2021/scavenger-hunt-4.png)


Si vamos al archivo veremos la tercera parte de la flag `t_0f_pl4c` y una pregunta. La respuesta a la pregunta es el archivo **.htaccess**.

![](/images/images-picoctf-2021/scavenger-hunt-5.png)

Si vamos al archivo .htaccess veremos la cuarta parte de la flag `3s_2_lO0k` y otra pregunta. La respuesta es el archivo **.DS_Store**.

![](/images/images-picoctf-2021/scavenger-hunt-6.png)

Si vamos al archivo veremos la última parte de la flag `_f7ce8828}`.

![](/images/images-picoctf-2021/scavenger-hunt-7.png)


## Respuesta a las preguntas

Saber googlear es una habilidad muy importante, acá te mostraré qué busquedas hice para encontrar las respuestas.


**Pregunta:**
- How can I keep Google from indexing my website?

**Respuesta:**

Practicamente copiamos y pegamos la pregunta en google y vemos una pregunta en **Stack Overflow**.

![](/images/images-picoctf-2021/scavenger-hunt-8.png)

![](/images/images-picoctf-2021/scavenger-hunt-10.png)

Vemos que en esta pregunta de **Stack Overflow** se hace mención al archivo robots.txt.


**Pregunta:**

- I think this is an apache server... can you Access the next flag?

**Respuesta:**

Podemos ver que la palabra Access está en mayúsculas, así que deberíamos agregar esa palabra a nuestra búsqueda.

![](/images/images-picoctf-2021/scavenger-hunt-9.png)

Vemos que en 6 occaciones se hace mención al archivo .htaccess. 


**Pregunta:**

- I love making websites on my Mac, I can Store a lot of information there.

**Respuesta:**

Las palabras **Mac** y **Store** están en mayúsculas, esto nos da una pista de cómo debemos hacer nuestra búsqueda. 

![](/images/images-picoctf-2021/scavenger-hunt-11.png)


# Flag
---

`picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_f7ce8828}`

---

## [Anterior](/cookies)
## [Siguiente](/some-assembly-required-1)