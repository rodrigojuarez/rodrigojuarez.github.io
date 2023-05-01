---
id: 11594
title: 'Ejecutar aplicaciones en forma segura con Windows Sandbox'
date: '2022-01-28T01:58:08-03:00'
author: 'Rodrigo Juarez'
layout: revision
guid: 'https://blog.rodrigojuarez.com/?p=11594'
permalink: '/?p=11594'
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

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/01/image.png?resize=662%2C582&ssl=1)<figcaption>Habilitar **Windows Sandbox**</figcaption></figure>Luego de reiniciar el equipo, ya tendremos acceso a la aplicacion.

## Uso

Luego de iniciar el Sandbox, podemos arrastrar cualquier archivo ejecutable desde el host a la ventana, y luego ejecutar la aplicacion.

Una vez que hemos finalizado nuestras pruebas, y previa confirmacion, cerramos el sandbox y todo el contenido sera borrado.

## Configuracion avanzada

En [este post](https://blog.rodrigojuarez.com/2022/01/28/configuracion-avanzada-de-windows-sandbox/) podemos ver ademas como crear archivos de configuracion.

## Referencias

La [documentacion oficial](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-sandbox/windows-sandbox-overview) de **Windows Sandbox.**