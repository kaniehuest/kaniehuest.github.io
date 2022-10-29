---
title: Hack The Boo 2022 - Juggling Facts
layout: post
description: La resolución del reto "Juggling Facts" del CTF "Hack The Boo 2022" organizado por Hack The Box.
tags:
- HackTheBox
- JugglingFacts
- ctf
- post
- writeups
---
# Descripción
---

An organization seems to possess knowledge of the true nature of pumpkins. Can you find out what they honestly know and uncover this centuries-long secret once and for all?

# Solución
---

El cuarto reto web del CTF nos presenta con unos "Spooky Facts" sobre calabazas xD.

![](/images/images-hacktheboo2022/jf-1.png)

Si hacemos click en el botón **Spooky Facts** vemos unos hechos aterradores.

![](/images/images-hacktheboo2022/jf-2.png)

Si hacemos click en el botón **Not So Spooky Facts** las página nos muestra unos hechos no tan aterradores como los anteriores.

![](/images/images-hacktheboo2022/jf-3.png)

Y si presionamos el tercer botón **Secret Facts** la página nos dice que los secretos solo pueden ser vistos per el **admin**.

![](/images/images-hacktheboo2022/jf-4.png)

No hay más funcionalidades que estas, así que vamos a leer el código fuente de la aplicación y rápidamente nos encontramos con que los datos aterradores están almacenados en una base de datos.

![](/images/images-hacktheboo2022/jf-5.png)

Si bajamos hasta el final nos encontramos con que la flag está almacenada en la base de datos.

![](/images/images-hacktheboo2022/jf-6.png)

Leyendo el códido fuente vemos que la página renderiza los **Spooky Facts** a través de una petición JSON, donde debemos indicar el tipo de **Fact** que queremos ver.

Primero verifica que exista un JSON con el key **type** y un valor, de no ser así ocurre un error.

Segundo mediante un switch compara el valor del **type** con 3 opciones: **secrets**, **spooky** y **not_spooky**.

![](/images/images-hacktheboo2022/jf-7.png)

Como vimos anteriormente en la base de datos, la flag tiene valor **secret**, así que debemos enviar un JSON con la key **type** y el valor **secrets**. Pero ocurre un problema, si indicamos el valor como **secrets** la aplicación realiza una comparación: nuestra ip debe ser 127.0.0.1.

![](/images/images-hacktheboo2022/jf-8.png)

Buscando en el código nos damos cuenta de que debemos realizar esta petición a la ruta `/api/getfacts`.

![](/images/images-hacktheboo2022/jf-9.png)

Yo usaré Postman para realizar las peticiones porque se me hace más cómodo, primero ingresamos la url y cambiamos el método a POST.

![](/images/images-hacktheboo2022/jf-10.png)

Luego vamos a la pestaña **Headers** y agregamos una nueva cabecera **Content-Type: application/json**.

![](/images/images-hacktheboo2022/jf-11.png)

Vamos a la pestaña **Body**, seleccionamos **raw**, ingresamos nuestro json con el valor **spooky** para comprobar que estamos realizando la petición correctamente y presionamos el botón **Send**.

![](/images/images-hacktheboo2022/jf-12.png)

La aplicación nos responde con contenido y un 200 OK.

![](/images/images-hacktheboo2022/jf-13.png)

Por muchas horas estuve intentado bypassear la comparación de la ip agregando cabeceras, esto solo fue un rabbit hole porque el reto no se soluciona por ahí.

![](/images/images-hacktheboo2022/jf-14.png)

Leyendo con más atención la descripción del reto y el título del reto me hizo click la palabra **juggling**, el título del reto es un hint para resolverlo. Procedo a buscar alguna comparación en el código donde se pueda explotar el **Type Juggling** pero no encuentro nada, el **if** que estabamos viendo no parece vulnerable.

![](/images/images-hacktheboo2022/jf-15.png)

Analizando el código un busca de comparaciones que sean vulnerables no encontraba nada, así que simplemente cambié el valor en el JSON de `"secrets"` a `true`, a ver si pasaba algo.

![](/images/images-hacktheboo2022/jf-16.png)

Por suerte obtuve la flag pero no entendía por qué hasta que leí la flag, el type juggling se puede abusar en la sentencia switch ya que por defecto switch en PHP hace una comparación `==` y no `===`.

![](/images/images-hacktheboo2022/jf-17.png)

Lo que pasa es que en la primera sentencia **if** se compara si el valor que enviamos es igual a **secrets** y que nuestra ip sea distinta a 127.0.0.1, al escribir **true** esta comparación no se cumple ya que nuestra ip SÍ es distinta a 127.0.0.1 pero el valor que enviamos NO es igual a **secrets**.

Luego en el switch la primera comparación que se realiza es `'secrets' == true` lo que es verdadero y procede a enviarnos la flag. Esta comparación no ocurre a plena vista, es algo interno de PHP y debido a esto el reto se vuelve tan complejo.

![](/images/images-hacktheboo2022/jf-18.png)


# Flag
---

`HTB{sw1tch_stat3m3nts_4r3_vuln3r4bl3!!!}`
