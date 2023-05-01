---
id: 11606
title: 'Creando un instalador offline para Visual Studio'
date: '2022-07-13T10:44:12-03:00'
author: 'Rodrigo Juarez'
layout: post
guid: 'https://blog.rodrigojuarez.com/?p=11606'
permalink: /2022/07/13/creando-un-instalador-offline-para-visual-studio/
jabber_published:
    - '1657719852'
timeline_notification:
    - '1657719852'
publicize_twitter_user:
    - rodrigojuarez
image: /wp-content/uploads/2022/07/0.jpg
categories:
    - 'Visual Studio'
tags:
    - 'Visual Studio'
---

Habitualmente trabajo con mas de una computadora para desarrollo y ademas hago reinstalaciones periodicas del sistema operativo, por lo que termino ocupando bastante tiempo descargando e instalando Visual Studio. Para facilitar esto, tenemos la posibilidad de utilizar el mismo archivo instalador que inicia el proceso interactivo de instalacion y agregando parametros podemos obtener una copia local de todos los archivos necesarios asi como automatizar los flujos o paquetes que deseamos instalar. Tambien podemos actualizar nuestro instalador offline para siempre tener la ultima version disponible y no tener que realizar todo el proceso cuando se publican nuevas versiones.

## Creando nuestro instalador offline

En este post voy a detallar paso a paso como realizar todas estas operaciones y voy a utilizar la version 2022 Community preview al momento de escribir esto. Otras versiones funcionan en forma similar, descargando el archivo instalador de dicha version. Siempre se pueden consultar los parametros ejecutando en la linea de comandos el archivo instalador con el parametro **-?** lo cual nos abrira una pagina web local temporal con toda la informacion

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/07/image.png?resize=782%2C617&ssl=1)</figure>Primero necesitamos obtener el archivo de instalacion desde la pagina de [descarga de Visual Studio](https://visualstudio.microsoft.com/es/vs/preview/#download-preview) y guardarlo en un directorio local, en mi caso utilizare **c:\\VSOffline**

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/07/image-1.png?resize=586%2C705&ssl=1)</figure>Luego debemos abrir una ventana de comandos en la carpeta en donde descargamos el instalador y ejecutar la siguiente instruccion que iniciara el (largo) proceso de descarga

```
<pre class="wp-block-code">```
`VisualStudioSetup --layout C:\VSOffline --lang en-US --add Microsoft.VisualStudio.Workload.NetCrossPlat --add Microsoft.VisualStudio.Workload.Universal --includeRecommended --includeOptional`
```
```

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/07/image-4.png?resize=771%2C589&ssl=1)</figure>Parametros utilizados

**–layout** es nuestra carpeta destino

**–lang** el lenguage a descargar, los posibles valores son los de la columna BCP 47 en el [siguiente enlace](https://docs.microsoft.com/en-us/openspecs/office_standards/ms-oe376/6c085406-a698-4e12-9d4d-c3b0ee3dbc4a)

**–includeRecommended** &amp; **–includeOptional** asegura que se descargan todos los archivos que necesitaremos al realizar la instalacion

**-add** los flujos que queremos esten incluidos en nuestro instalador. En mi caso estoy interesado solo en los flujos relacionados a desarrollo cross platform. Se puede seleccionar cualquiera de los disponibles, utilizando la lista de [posibles valores que se encuentra aqui.](https://docs.microsoft.com/en-us/visualstudio/install/workload-component-id-vs-community?view=vs-2022)

## Actualizar nuestro instalador offline

Si ya tenemos nuestra carpeta con los archivos de instalacion y deseamos actualizar a la ultima version cuando existen cambios, solo debemos volver a ejecutar la misma instruccion que usamos originalmente.

## Instalar visual studio

En la misma ventana de comandos en la que ejecutamos el comando para descarga, corremos la siguiente instruccion

```
<pre class="wp-block-code">```
VisualStudioSetup --passive --norestart --includeOptional
```
```

Esto iniciara el proceso de instalacion, como se puede ver en la siguiente captura de pantalla. Los archivos no son descargados nuevamente, solo se verifica que esten disponibles.

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/07/image-6.png?resize=782%2C362&ssl=1)</figure>Si abrimos el instalador, podemos ver que se instalaron correctamente los flujos deseados

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/07/image-7.png?resize=782%2C451&ssl=1)</figure>- - - - - -

En un proximo post, voy a agregar informacion sobre como se puede automatizar aun mas el proceso y ademas como podemos utilizarlo junto a [Windows Sandbox](https://blog.rodrigojuarez.com/2022/01/28/ejecutar-aplicaciones-en-forma-segura-con-windows-sandbox/) para crear rapidamente entornos de desarrollo repetibles y que se encuentran siempre en el mismo estado incial.

Espero les haya sido de utilidad y les permita configurar sus equipos de desarrollo rapidamente!