---
title: Hack This Site - Chicago American **** Party
layout: post
post-image: /assets/images/perropc1.jpg 
description: La resolución del reto Chicago American **** Party. 
tags:
- hackthissite
- realistic
- post
- writeups
---
# Descripción
---

Message: I have been informed that you have quite admirable hacking skills. Well, this racist hate group is using [their website](https://www.hackthissite.org/missions/realistic/2) to organize a mass gathering of ignorant racist bastards. We cannot allow such bigoted aggression to happen. If you can gain access to their administrator page and post messages to their main page, we would be eternally grateful.


# Solución
---

En la página principal no se observa nada importante más que un montón de imágenes y palabras que tuve que censurar jajajaj.

![](/images/images-hts-realistic/lab2-1.png)

Vemos el código fuente presionando `CTRL + u` y observamos un archivo `update.php` al final de la página, nuevamente tuve que censurar muchas palabras.

![](/images/images-hts-realistic/lab2-2.png)

Si navegamos a ese archivo observamos un panel de inicio de sesión.

![](/images/images-hts-realistic/lab2-3.png)

Ingresamos una inyección SQL en el campo de username, luego hacemos click en el botón **Submit Query** y resolvemos el reto.

```sql
' or 1=1 -- -
```

![](/images/images-hts-realistic/lab2-4.png)

