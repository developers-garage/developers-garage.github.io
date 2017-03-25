---
title: "Android Things lector de codigo de barras"
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


En este articulo vamos a ver como usar un lector de codigo con Android Things, para ello utilizaremos una Raspberry Pi y un lector Datalogic GFS4400.

#### ¿Que necesitamos?

* 1 x Rasberry Pi 3 Model B
* 1 x Tarjeta SD 8G class 10
* 1 X Lector de codigo de barras Datalogic GFS4400
* 1 X Plaxa adaptadora
* 1 X Cable serie cruzado

#### Software que utilizaremos

* Android Studio
* Android Things
* Conocimientos de programación Java y Android.

#### Paso 1: Instalar Android Things

Lo primero que necesitamos es tener una placa **Raspberry Pi 3 Model B** con Android Things instalado, si ya lo tines puedes saltarte este paso e ir directamante al Paso 2.

Para facilitar la grabación de la SD uitlizaremos el programa [Etcher](https://etcher.io/), comenzaremos por descargarlo e instalarlo. Tambien necesitarmos la ultima imagen de Android Things para Raspberry Pi, actualmente estan en la versión preview 2, podemos descargarla desde la página [Android Things](https://developer.android.com/things/index.html)

>Neceistaremos almenos una tarjeta de 4G de clase 10. Pero es recomendable una sd de 8G, para que nos queda suficiente espacio libre para instalar aplicaciones.

La primera pantalla que veremos de Etcher nos pide donde tenemos descargada la imagen de Android Things, no es necesario descromprimir el zip que hemos decargado, Etcher se encargara de todo.

![Etcher seleccionar archivo de imagen](/images/2017/03/android-things-barcode/etcher-01-min.png)

![Etcher seleccionar unidad tarjeta sd](/images/2017/03/android-things-barcode/etcher-02-min.png)

Ahora ya tenemos la SD con el sistema instalado, podemos insertarla en la Raspberry Pi, conectar el cable de red a nuestro router y arrancar, al ser la primra vez os aconsejo que conecteis un monitor para ver que todo funciona correctamente, tambien nos servira para ver la IP que asigana.

> Para programar Android Things tendremos que conectar por red (cable, wifi) y usar el programa adb.

#### Paso 2: Desactivar Depuración Puerto Serie

#### Paso 3: Adaptador RS232 para Raspberry Pi

#### Paso 4: Lector de Código de barras

#### Paso 5: Cruzador RS232

#### Paso 6: Codigo App Android Things

#### Paso 7: Pruebas 

#### Esquema

#### Fuentes