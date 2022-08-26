---
title: PicoCTF 2022 - SQL Direct 
layout: post
post-image: /assets/images/gatohacker3.jpeg 
description: Resolución del reto SQL Direct. 
tags:
- picoctf
- ctf
- picoctf2022
- post
- writeups
---
# Descripción
---

Connect to this PostgreSQL server and find the flag!


# Hints
---

- What does a SQL database contain?


# Solución
---

Primero debemos conectarnos a la base de datos con el comando y contraseña que nos entrega la página.

![](/assets/images/images-picoctf-2022/sql-direct-1.png)

Cuando entremos en la base de datos escribimos `\d` para listar las tablas que existen. Podemos ver una que se llama **Flags**.

![](/assets/images/images-picoctf-2022/sql-direct-2.png)

Para listar el contenido de esta tabla usamos el siguiente comando:

```sql
select * from flags;
```

Y podemos ver la flag.

![](/assets/images/images-picoctf-2022/sql-direct-3.png)


# Flag
---

`picoCTF{L3arN_S0m3_5qL_t0d4Y_73b0678f}`

---

## [Anterior](/blog/Secrets)
## [Siguiente](/blog/SQLiLite)