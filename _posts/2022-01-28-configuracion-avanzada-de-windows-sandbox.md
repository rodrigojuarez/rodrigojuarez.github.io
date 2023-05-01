---
id: 11584
title: 'Configuracion avanzada de Windows Sandbox'
date: '2022-01-28T01:45:49-03:00'
author: 'Rodrigo Juarez'
layout: post
permalink: /2022/01/28/configuracion-avanzada-de-windows-sandbox/
image: /wp-content/uploads/2022/01/pexels-photo-4160347.jpeg
categories:
    - Backend
    - Pruebas
tags:
    - Development
    - Virtualization
    - 'Windows Sandbox'
---

En un [post anterior](https://blog.rodrigojuarez.com/2022/01/28/ejecutar-aplicaciones-en-forma-segura-con-windows-sandbox/) comento como instalar y la utilizacion basica de **Windows Sandbox.**

Si comenzamos a utilizarlo habitualmente, veremos que debido a la reinicializacion total, estaremos repitiendo ciertos pasos cada vez que iniciamos la aplicacion.

Para evitar algunos de estos pasos repetitivos, podemos utilizar un archivo de configuracion. **Windows Sandbox** nos permite escribir archivos de configuracion, formateados como XML, los mismos utilizan la extension **.wsb**.

Utilizando cualquier editor de texto que nos permita trabajar con texto plano, podemos crear nuestro archivo de configuracion.

En el siguiente archivo de configuracion de ejemplo, vemos las opciones que tenemos disponibles, como la posibilidad de mapear una carpeta de la maquina host en una carpeta del Sandbox, o ejecutar un comando en el sandbox luego de que inicia. En el ejemplo, estamos ademas iniciando la instalacion de Visual Studio Community 2022 que ya tenemos previamente descargado en la computadora host.

```
<Configuration>
    <vGPU>Default</vGPU><!--Enable|Disable|Default-->
    <Networking>Default</Networking><!--Disable|Default-->
    <MappedFolders>
        <MappedFolder> 
            <HostFolder>D:\VS\Preview\Community2022</HostFolder><!--absolute path to the host folder-->
            <SandboxFolder>C:\VS</SandboxFolder><!--absolute path to the sandbox folder-->
            <ReadOnly>false</ReadOnly> <!--true|false-->
        </MappedFolder>
    </MappedFolders>
    <LogonCommand>
        <Command>C:\VS\vs_community.exe --passive --norestart --includeOptional</Command> <!--command to be invoked-->
    </LogonCommand>
    <AudioInput>Default</AudioInput><!--Enable|Disable|Default-->
    <VideoInput>Default</VideoInput><!--Enable|Disable|Default-->
    <ProtectedClient>Default</ProtectedClient><!--Enable|Disable|Default-->
    <PrinterRedirection>Default</PrinterRedirection><!--Enable|Disable|Default-->
    <ClipboardRedirection>Default</ClipboardRedirection><!--Disable|Default-->
    <MemoryInMB>4096</MemoryInMB>
</Configuration>
```

Luego de guardar el archivo en nuestro disco local con la extension .wsb podemos hacer doble click sobre el mismo, lo que iniciara **Windows Sandbox** y cargara las opciones establecidas.

Podemos de esta manera tener distintos archivos de configuracion que nos daran acceso a diferentes configuraciones de prueba en forma muy rapida y sencilla.

Aqui les dejo el enlace a la [documentacion oficial](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-sandbox/windows-sandbox-configure-using-wsb-file) para que puedan ver los detalles de los distintos parametros.