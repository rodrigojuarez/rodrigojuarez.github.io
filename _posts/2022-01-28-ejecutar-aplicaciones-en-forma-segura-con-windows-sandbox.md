---
id: 11572
title: 'Ejecutar aplicaciones en forma segura con Windows Sandbox'
date: '2022-01-28T01:13:35-03:00'
author: 'Rodrigo Juarez'
layout: post
permalink: /2022/01/28/ejecutar-aplicaciones-en-forma-segura-con-windows-sandbox/
image: /wp-content/uploads/2022/01/pexels-photo-7862529.jpeg
categories:
    - Backend
    - Pruebas
tags:
    - Pruebas
    - Sandbox
    - 'Sistema Operativo'
---

Windows Sandbox es un entorno que nos permite ejecutar aplicaciones en forma segura y aislada de la computadora host.

Cualquier software que necesitemos, debe ser instalado cada vez que el sandbox se inicia.

## Ventajas

Esta incluido en Microsoft Windows 10 y 11, por lo que no necesita la descarga de software adicional.

Cada vez que se inicia, nos da una nueva instalacion del sistema operativo.

Es seguro, utiliza virtualizacion basada en hardware para aislar el sandbox de la computadora host.

Es eficiente, consumiendo menos recursos que maquinas virtuales.

## Requisitos

Windows 10/11 Pro/Enterprise

Arquitectura AMD64

Virtualization habilitada en la BIOS

Al menos 4 GB de RAM

Al menos 1 GB de espacio libre en disco

Al menos CPU de dos nucleos

## Instalacion

Habilitar la virtualizacion

En la seleccion de caracteristicas de Windows, habilitar **Windows Sandbox**

![](/wp-content/uploads/2022/01/image.png?resize=662%2C582&ssl=1)
Habilitar **Windows Sandbox**

Luego de reiniciar el equipo, ya tendremos acceso a la aplicacion.

## Uso

Luego de iniciar el Sandbox, podemos arrastrar cualquier archivo ejecutable desde el host a la ventana, y luego ejecutar la aplicacion.

Una vez que hemos finalizado nuestras pruebas, y previa confirmacion, cerramos el sandbox y todo el contenido sera borrado.

## Configuracion avanzada

En [este post](/2022/01/28/configuracion-avanzada-de-windows-sandbox/) podemos ver ademas como crear archivos de configuracion.

## Referencias

La [documentacion oficial](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-sandbox/windows-sandbox-overview) de **Windows Sandbox.**