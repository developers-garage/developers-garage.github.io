---
title: "Android Things UART y Lector de codigo de barras"
description: "Como conectar y leer codigos de barras con Android Things"
date: "2017-03-18"
draft: false
slug: "android-things-codigo-barras"
categories:
    - "post"
tags:
    - "raspberry pi"
    - "android things"

# metadata specific Theme
image: "images/2014/Jul/titledotscale.png"
comments: true     # set false to hide Disqus comments
share: true        # set false to share buttons
menu: ""           # set "main" to add this content to the main menu

#cardimagelg: "/images/default.jpg"
#cardimagesm: "/images/default.jpg"
#cardbackground: "#263654" #optional: overwrites default #263238, only shows when no image specified.
"author":
    name: "Jose A. Luceño"
    description: "Writer of stuff"
    website: "http://example.com/"
    email: "firstname@example.com"
    twitter: "https://twitter.com/"
    github: "https://github.com/"
    image: "/images/avatar-64x64.png"
---


En este articulo vamos a ver como usar el UART o puerto serie que incorpora la Raspberry Pi. Como ejemplo usaremos un lector de codigo de barras Datalogic GFS4400.

#### ¿Que necesitamos?

* 1 x Rasberry Pi 3 Model B con Android Things
* 1 X Lector de codigo de barras Datalogic GFS4400
* 1 X Placa adaptadora
* 1 X Cable serie cruzado DB9

#### Software que utilizaremos

* Android Studio
* Android Things
* Conocimientos de programación Java y Android.

Antes de empezar te recomendamos que eches un vistazo al articulo [Android Things Comenzando](), donde podras preparar la base para seguir este articulo.

#### Paso 1: Desactivar Depuración Puerto Serie

Por defecto la UART de la Raspberry Pi se utiliza para depuración, para evitar conflictos en nuestros proyectos, tendremos que desactivar la depuración.

Sacaremos la tarjeta SD de la Raspberry Pi y la conectaremos a nuestro ordenador, buscamos el archivo cmdline.txt y el parametro console lo dejaremos de este modo

```
console=tty0
```
Guardamos el fichero y colocamos de nuevo la SD en la Raspberry Pi.

#### Paso 2: Adaptador RS232 para Raspberry Pi

La UART de la Raspberry Pi funciona con niveles de tensión TTL a 3.3v, debemos tener cuidado de no conectar dispositivos que superen el voltaje. En el ejemplo que mostraremos usamos un lector con con niveles de +/-12v por eso utilizamos una placa que adpta los nivelez de voltaje, es muy fácil de conseguir por Internet.

IMAGEN DE LA TARJETA

Para conectar la placa de adaptació a la Raspberry Pi lo haremos siguiendo este esquema.

ESQUEMA DE CONEXION


#### Paso 3: Lector de código de barras

#### Paso 4: Cruzando TX y RX

En este ejemplo utilizaremos la comunicación con tres hilos, necesitaremos cruzar los pins TX y RX del lector con los de la Raspberry, auque podemos conseguir comprar un cable cruzado en alguna tienda de electronica, hemos decido hacernos uno.

Sigúendo este esquema y dos conectores DB9 macho.

ESQUEMA DEL CABLE

Nos queda el siguiente montaje

FOTO DEL MONTAJE


#### Paso 5: Codigo App Android Things

Con todo montado podemos empezar la parte de programación, suponiendo que partimos de un proyecto para Android Things correctamente cofigurado.



#### Paso 6: Pruebas 

#### Fuentes