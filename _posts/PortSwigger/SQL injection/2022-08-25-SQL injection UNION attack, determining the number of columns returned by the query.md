---
title: PortSwigger - SQL injection UNION attack, determining the number of columns returned by the query.
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto SQL injection UNION attack, determining the number of columns returned by the query. 
tags:
- portswigger
- sqli
- post
- writeups
---
# Solución
---

En la página principal hacemos click en alguna opción de búsqueda, yo voy a hacerle click a **Lifestyle**.

![](/images/images-portswigger-sqli/lab3-1.png)

Luega se agregará a la url un filtro que busca según lo que escogiste, en este caso como escogimos **Lifestyle** nos muestro `filter?=category=Lifestyle`.

![](/images/images-portswigger-sqli/lab3-2.png)

Al final debemos agregar una query SQL para identificar la cantidad de columnas que existen. Primero escribimos `' union select null -- -` y si la página nos devuelve un error entonces seguimos agregando la palabra `null` hasta que se arregle.

![](/images/images-portswigger-sqli/lab3-3.png)

Con un solo `null` nos devuelve un error, esto significa que existen más de 1 columna.

```sql
' UNION SELECT null -- -
```

![](/images/images-portswigger-sqli/lab3-4.png)

Con 2 `null` también nos devuelve un error, entonces debemos agregar más `null`.

```sql
' UNION SELECT null,null -- -
```

![](/images/images-portswigger-sqli/lab3-5.png)

Si agregamos 3 `null` el laboratorio se resuelve porque existen 3 columnas.

```sql
' UNION SELECT null,null,null -- -
```

![](/images/images-portswigger-sqli/lab3-6.png)

---

## [Anterior](/SQL-injection-vulnerability-allowing-login-bypass)
## [Siguiente](/SQL-injection-UNION-attack%2C-finding-a-column-containing-text)