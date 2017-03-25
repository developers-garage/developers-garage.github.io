---
title: "Android Things Comenzando"
description: "Cómo conectar y leer códigos de barras con Android Things"
date: "2017-03-17"
draft: false
slug: "android-things-comenzando"
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
    website: "http://www.jalcdeveloper.com/"
    email: "jalcuenyo@gmail.com"
    github: "https://github.com/jalucenyo"
    image: "/images/avatar-64x64.png"
---

En este primer artículo de la serie Android Things comenzaremos por flashear una Raspberry Pi con una imagen de Android Things, configurar la conexión a nuestra red Wifi y para terminar el artículo crearemos nuestra primera App "Hola Mundo".

#### ¿Que necesitamos?

* 1 x Raspberry Pi 3 Model B
* 1 x Tarjeta micro SD 8G class 10
* 1 x Adaptador microSD a USB

#### Software que utilizaremos

* Android Things
* Android Studio
* Conocimientos de programación Java y Android.

#### Paso 1: Instalar Android Things

Lo primero que necesitamos es tener una placa **Raspberry Pi 3 Model B** con Android Things instalado, si ya lo tienes puedes saltarte este paso e ir directamente al Paso 2.

Para facilitar la grabación de la SD utilizaremos el programa [Etcher](https://etcher.io/), comenzaremos por descargarlo e instalarlo. También necesitaremos la última imagen de Android Things para Raspberry Pi, actualmente están en la versión preview 2, podemos descargarla desde la página [Android Things](https://developer.android.com/things/index.html)

>Necesitaremos al menos una tarjeta de 4G de clase 10. Pero es recomendable una sd de 8G, para que nos queda suficiente espacio libre para instalar aplicaciones.

La primera pantalla que veremos de Etcher nos pide donde tenemos descargada la imagen de Android Things, no es necesario descomprimir el zip que hemos descargado, Etcher se encargará de todo.

![Etcher seleccionar archivo de imagen](/images/2017/03/android-things-comenzando/etcher-01-min.png)

Ahora conectamos la tarjeta SD a nuestro ordenador.

![Etcher tarjeta sd](/images/2017/03/android-things-comenzando/etcher-02-min.png)

Etcher detecta automáticamente la tarjeta y únicamente tenemos que pulsar en el botón "Flash"

![Etcher comenzar a grabar](/images/2017/03/android-things-comenzando/etcher-03-min.png)

Aproximadamente tardará unos 10-15 minutos en grabar la imagen, ya que también hace un proceso para comprobar que la imagen se ha grabado correctamente.

![Etcher comenzar a grabar](/images/2017/03/android-things-comenzando/etcher-04-min.png)

Una vez finalizado podemos extraer la tarjeta del ordenador.

![Etcher finalizado](/images/2017/03/android-things-comenzando/etcher-flash-finish-min.png)

Colocaremos la tarjeta en la Raspberry Pi, conectaremos un cable HDMI a un monitor, también conectaremos el cable de red a nuestro router o switch y por último alimentamos la Raspberry Pi. 

![Raspberry Pi Conexiones](/images/2017/03/android-things-comenzando/raspberry-pi-connected-min.jpg)

Tras unos segundos podemos ver la pantalla de arranque, en la que nos muestra la ip que nuestro router le ha asignado.

![Android Things Pantalla](/images/2017/03/android-things-comenzando/android-things-start-min.jpg)


#### Paso 2: Conectando

Para poder programar nuestra Raspberry Pi con Android Things debe estar conectado a una red, no podemos programarla por usb como se suele hacer con un móvil Android. Usaremos "Android Debug Bridge" o [adb](https://developer.android.com/studio/command-line/adb.html?hl=es-419), que nos permitira conectarnos, enviar aplicaciones y depurar los programas.

Ejecutaremos el siguiente comando desde una consola, en nuestro equipo. 

```
adb connect 192.168.2.114
```

Si todo ha ido bien nos responderá.

```
adb connected to 192.168.2.114:5555
```
De este modo ya estamos conectados y listos para poder hacer nuestra primera aplicación.

> Para programar Android Things tendremos que conectar por red (cable, wifi) y usar el programa adb.


#### Paso 3: Configuración de la Wifi (Opcional)

Como sabéis Raspberry Pi 3 lleva integrada el módulo wifi y está soportado por Android Things, podemos conectar con una red wifi y asi no depender del cable de red. Para configurarlo utilizaremos el siguiente comando:

```
adb shell am startservice ^
    -n com.google.wifisetup/.WifiSetupService ^
    -a WifiSetupService.Connect ^
    -e ssid <Network_SSID> ^
    -e passphrase <Network_Passcode>
```

<Network_SSID> lo sustituimos el el nombre de la red Wifi.
<Network_Passcode> indicamos la contraseña de la red Wifi.
Para los usuarios de linux sustituir el carácter ^ por \

Podemos comprobar si la ha podido conectarse revisando los logs con el comando

```
adb logcat -d
```

Nos mostrará todos los logs del sistema y veremos unas líneas que indican

```
WifiWatcher: Network state changed to CONNECTED
WifiWatcher: SSID changed: <Network_SSID>
```

Los logs pueden tener cientos de líneas así que podemos filtrarlos del siguiente modo.

Windows
```
adb logcat -d  | findstr /R /C:"Wifi"
```

Linux
```
adb logcat -d | grep Wifi
```

>La configuración de la wifi quedará guardada y cada vez que arranquemos la Raspberry Pi automáticamente intentará conectarse.

En la pantalla conectada a la Raspberry Pi, veremos la ip que nos ha asignado el router wifi. Ahora desconectamos el adb con el comando:

```
adb disconnect
``` 

Y nos conectaremos nuevamente con la ip que nos ha asignado en la red wifi.

```
adb connect 192.168.3.80
```

En este momento ya podemos conectar el cable de red de la Raspberry Pi. Por último para asegurarnos que todo funciona correctamente podemos comprobar que la Raspberry Pi tiene conexión con el comando:

```
adb shell ping 8.8.8.8
```
Con Ctrl+C podemos parar el ping.


#### Paso 4: App Android Things - Hello World!!

Después de tanta configuración llegamos a la parte interesante, que es crear nuestra primera App para Android Things. Veréis que es prácticamente igual que crear una App para otras plataformas de Android, ya sea móvil, tv, auto.

Lo primero es abrir Android Studio y crear un nuevo proyecto con el API 24.

![Android Studio API](/images/2017/03/android-things-comenzando/android-studio-new-proyect-api.png)

>Como Android Things, en el momento de escribir este artículo, es una preview Android Studio no está del todo automatizado por lo que deberemos añadir algunas cositas a mano.


En el archivo build.gradle a nivel de la app, añadiremos la siguiente línea dentro de la sección dependencies.

```
 provided 'com.google.android.things:androidthings:0.2-devpreview'
```
Para aplicar los cambios clicamos en "Sync Now", Android Studio se encargará de bajar las dependencias.

En el archivo de AndroidManifest.xml dentro de la sección "application" añadimos la siguiente línea.

```
<uses-library android:name="com.google.android.things"/>

```

Finalmente dentro de la sección de declaración de la "activity" principal o inicial incluimos un intent-filter como el siguiente, este indica cual es la aplicación que arrancará automáticamente cuando encendemos la Raspberry Pi. 

```
<!-- Launch activity automatically on boot -->
<intent-filter>
    <action android:name="android.intent.action.MAIN"/>
    <category android:name="android.intent.category.IOT_LAUNCHER"/>
    <category android:name="android.intent.category.DEFAULT"/>
</intent-filter>
```

> Al tratarse de una plataforma pensada para el Internet de las Cosas, Android Things no tienen una interfaz de usuario donde podamos cambiar de aplicaciones, el interface gráfico queda en manos del desarrollador.

Por último solo nos queda enviar y ejecutar la aplicación, clicando en el botón "Run App" el famoso Play verde. Nos aparece la ventana con la lista de dispositivos, seleccionamos la Raspberry y esperamos a que termine el proceso de envío y ejecución.

En breve veremos aparecer la aplicación con el texto Hello World.

Hemos llegado al final de este artículo, de la serie Android Things dejando la base preparada. En los próximos artículos veremos cómo utilizar el puerto serie, usar las GPIO para controlar relés, leds y pulsadores, controlar servos y I2C
