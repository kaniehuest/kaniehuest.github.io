---
title: PicoCTF 2021 - Who are you?
layout: post
post-image: /assets/images/gatohacker3.jpeg 
description: Resolución del reto Who are you?
tags:
- picoctf
- ctf
- picoctf2021
- post
- writeups
---
# Descripción
---

Let me in. Let me iiiiiiinnnnnnnnnnnnnnnnnnnn 


# Hints
---

- It ain't much, but it's an RFC https://tools.ietf.org/html/rfc2616


# Solución
---

Primero vamos a Burpsuite y abrimos el navegador.

![](/images/images-picoctf-2021/who-are-you-1.png)

En el navegador vamos a la página del reto.

![](/images/images-picoctf-2021/who-are-you-2.png)

Hacemos click en el botón **Intercept is off** para que cambie a **Intercept is on** y así poder interceptar la petición con la que vamos a trabajar.

![](/images/images-picoctf-2021/who-are-you-3.png)

![](/images/images-picoctf-2021/who-are-you-4.png)

Vamos al navegador, recargamos la página y vemos la petición en Burpsuite. Después hacemos click derecho sobre la petición y la enviamos al **Repeater**.

![](/images/images-picoctf-2021/who-are-you-5.png)

Nos vamos a la pestaña **Repeater**, hacemos click en **Send** y debajo de **Response** nos vamos a la pestaña  **Render**.

![](/images/images-picoctf-2021/who-are-you-6.png)

La página nos dice que nuestro navegador debe ser **PicoBrowser**, entonces debemos cambiar el header **User-Agent** para que diga **PicoBrowser**.

![](/images/images-picoctf-2021/who-are-you-7.png)

Después de cambiar el **User-Agent** y hacer click en **Send**, la página nos dice que no confía en usuarios que vengan de otro sitio.

![](/images/images-picoctf-2021/who-are-you-8.png)

Como nos dice que debemos venir desde el mismo sitio, agregamos una cabecera llamada **Referer** y le colocamos la misma dirección de la cabecera **Host**.
 
![](/images/images-picoctf-2021/who-are-you-9.png)

Ahora nos dice que el sitio solo funcionaba en el 2018.

![](/images/images-picoctf-2021/who-are-you-10.png)

Para resolver esto, le agregamos otra cabecera llamada **Date**, le agregamos una fecha como la que coloqué yo, y que tenga de año el 2018. Finalmente hacemos click en el botón **Send**.

![](/images/images-picoctf-2021/who-are-you-11.png)

Ahora nos dice que la página solo acepta gente de Suecia.

![](/images/images-picoctf-2021/who-are-you-12.png)

Necesitamos agregar otra cabecera llamada **X-Forwarded-For** y agregar cualquier dirección **ip** de Suecia. 

![](/images/images-picoctf-2021/who-are-you-13.png)

Hacemos click en el botón **Send** y ahora la página nos pregunta que por qué no hablamos sueco.

![](/images/images-picoctf-2021/who-are-you-14.png)

Para solucionar esto agregamos las siglas **sv** al final de la cabecera **Accept-Language** separado por una coma.

![](/images/images-picoctf-2021/who-are-you-15.png)

Hacemos click en el botón **Send** y podemos ver la flag.

![](/images/images-picoctf-2021/who-are-you-16.png)

Para copiarla simplemente nos vamos a la pestaña **Raw** que está a la izquierda de **Render** y bajamos un poco.

![](/images/images-picoctf-2021/who-are-you-17.png)


# Flag
---

`picoCTF{http_h34d3rs_v3ry_c0Ol_much_w0w_b22d773c}`

---

## [Anterior](/some-assembly-required-1)