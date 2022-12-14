---
title: PortSwigger - SQL injection UNION attack, finding a column containing text.
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto SQL injection UNION attack, finding a column containing text. 
tags:
- portswigger
- sqli
- post
- writeups
---
# Solución
---

En la página principal podemos ver un mensaje que nos indica un mensaje, el cual debemos mostrar en la página web a través de la base de datos, o sea, a través de nuestra SQL injection.

El mensaje es `wKtwyV`.

![](/images/images-portswigger-sqli/lab4-1.png)

Luego haremos click en un filtro de búsqueda, en mi caso haré click en `Gifts`.

![](/images/images-portswigger-sqli/lab4-2.png)

Observamos que en la url se agrega un filtro `filter?category=Gifts`.

![](/images/images-portswigger-sqli/lab4-3.png)

Primero debemos enumerar el número de columnas que existen, para eso comenzamos con un `null` y seguimos agregando hasta que la página nos responda correctamente, en este caso con un solo `null` la página se rompe.

```sql
' UNION SELECT null -- -
```

![](/images/images-portswigger-sqli/lab4-4.png)

Si agregamos dos `null` también nos devuelve un error.

```sql
' UNION SELECT null,null -- -
```


![](/images/images-portswigger-sqli/lab4-5.png)

Si agregamos tres `null` la página nos responde correctamente, esto significa que existen tres columnas.

```sql
' UNION SELECT null,null,null -- -
```

![](/images/images-portswigger-sqli/lab4-6.png)

Después de enumerar las columnas, hay que enumerar la columna que acepta strings, para eso cambiamos un null por una string entre comillas.

```sql
' UNION SELECT 'a',null,null -- -
```

Podemos ver que la primera columna ha sido cambiada por una string `'a'` pero la página nos devuelve un error, esto significa que la primera columna no acepta strings.

![](/images/images-portswigger-sqli/lab4-7.png)

Entonces cambiamos la primera columna devuelta a `null` y modificamos el segundo `null` para que ahora sea una string `'a'`

```sql
' UNION SELECT null,'a',null -- -
```

Esta vez podemos ver que la página nos responde correctamente y que muestra nuestra letra `a` en la página al final.

![](/images/images-portswigger-sqli/lab4-8.png)

Finalmente cambiamos la letra `a` por la cadena que nos señalaba la página al principio `# wKtwyV` y resolvemos el lab.

```sql
' UNION SELECT null,'wKtwyV',null -- -
```

![](/images/images-portswigger-sqli/lab4-9.png)


---

## [Anterior](/sql-injection-union-attack-determining-the-number-of-columns-returned-by-the-query)
## [Siguiente](/sql-injection-union-attack-retrieving-data-from-other-tables)