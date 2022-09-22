---
title: PortSwigger - Blind SQL injection with time delays 
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Blind SQL injection with time delays.
tags:
- portswigger
- sqli
- post
- writeups
---
# Solución
---

Vamos a la página principal.

![](/images/images-portswigger-sqli/lab13-1.png)

Hacemos click derecho y seleccionamos **Inspeccionar**.

![](/images/images-portswigger-sqli/lab13-2.png)

Luego vamos a la pestaña **Application**, vamos a cookie y vemos la cookie que es vulnerable a SQLi.

![](/images/images-portswigger-sqli/lab13-3.png)

Editamos el valor de la cookie y agregamos `'||pg_sleep(10)-- -`. **pg_sleep** es una función de PostgreSQL para esperar un determinado tiempo, agregandole el número 10 le indicamos que queremos esperar 10 segundos como nos dice en la descripción del reto.

![](/images/images-portswigger-sqli/lab13-8.png)

Guardamos y cuando recarguemos la página se demorará un poco más de 10 segundo, cuando termine de cargar tendremos el laboratorio resuelto.

![](/images/images-portswigger-sqli/lab13-9.png)

---

## [Anterior](/blind-sql-injection-with-conditional-responses)