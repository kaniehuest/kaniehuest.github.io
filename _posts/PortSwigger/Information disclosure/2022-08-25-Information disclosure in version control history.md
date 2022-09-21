---
title: PortSwigger - Information disclosure in version control history (sin Burpsuite).
layout: post
post-image: /assets/images/gatohacker4.jpg 
description: La resolución del reto Information disclosure in version control history.
tags:
- portswigger
- information-disclosure
- post
- writeups
---
# Solución
---

Primero vamos a la console y ejecutamos el siguiente comando para copiar toda la carpeta `.git` a nuestro escritorio.

```bash
wget -r linkdellaboratorio
```

![](/images/images-portswigger-id/lab5-1.png)

Cuando termine de descargar entramos a la carpeta.

```bash
cd nombredelacarpeta
```

![](/images/images-portswigger-id/lab5-2.png)

Entramos a la carpeta `.git`.

```bash
cd .git
```

![](/images/images-portswigger-id/lab5-3.png)

Ejecutamos el siguiente comando  para ver los commits.

```bash
git log
```

Podemos notar que en el mensaje del commit nos indica que se ha eliminado la contraseña de admin en un archivo config.

![](/images/images-portswigger-id/lab5-4.png)

Ejecutamos el siguiente comando para visualizar los cambios que se realizar en el último commit.

```bash
git show hashdelcommit
```

![](/images/images-portswigger-id/lab5-5.png)

Observamos que se eliminó la contraseña de admin y se reemplazó por **env('ADMIN_PASSWORD')**.

![](/images/images-portswigger-id/lab5-6.png)

Vamos a la página web del reto y hacemos click en el botón **My account**.

![](/images/images-portswigger-id/lab5-7.png)

Ingresamos el usuario administrador y la contraseña que obtuvimos en el commit.

![](/images/images-portswigger-id/lab5-8.png)

Si todo salió correctamente inicamos sesión como administrador.

![](/images/images-portswigger-id/lab5-10.png)

Hacemos click en el botón **Admin panel**.

![](/images/images-portswigger-id/lab5-11.png)

Eliminamos al usuario carlos.

![](/images/images-portswigger-id/lab5-12.png)

Y terminamos el laboratorio.

![](/images/images-portswigger-id/lab5-13.png)


---

## [Anterior](/authentication-bypass-via-information-disclosure)