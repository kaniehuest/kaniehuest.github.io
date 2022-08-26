---
title: CTFlearn - Basic Injection
layout: post
post-image: /assets/images/gatohacker2.jpeg 
description: La resolución del reto Basic Injection.
tags:
- ctflearn
- post
- writeups
---
# Descripción
---

See if you can leak the whole database using what you know about SQL Injections. 


# Solución
---

En la página podemos ver un campo de input donde debemos escribir una SQLi para obtener la flag.

![](/assets/images/images-ctflearn/basic-injection-1.png)

Escribimos una query muy simple `' or 1=1-- -`. 

![](/assets/images/images-ctflearn/basic-injection-2.png)

Y podemos ver la flag en el resultado.

![](/assets/images/images-ctflearn/basic-injection-3.png)


# Flag
---

`CTFlearn{th4t_is_why_you_n33d_to_sanitiz3_inputs}`

---

## [Siguiente](/blog/POST-Practice)