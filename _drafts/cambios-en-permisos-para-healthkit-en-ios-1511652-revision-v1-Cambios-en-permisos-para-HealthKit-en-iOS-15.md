---
id: 11657
title: 'Cambios en permisos para HealthKit en iOS 15'
date: '2022-08-03T11:28:37-03:00'
author: 'Rodrigo Juarez'
layout: revision
guid: 'https://blog.rodrigojuarez.com/?p=11657'
permalink: '/?p=11657'
---

Estuve recientemente actualizando las librerias de una aplicacion desarrollada en Xamarin.Forms que hace bastante tiempo se encuentra finalizada y que accede a datos de salud y actividad fisica en iOS.

Una de las librerias a actualizar fue la libreria de terceros que es la encargada de tomar los datos de HealthKit y prepararlos para ser enviados al servidor.

Luego de la actualizacion, comprobe que la sincronizacion seguia funcionando y enviamos la aplicacion a los usuarios.

La aplicacion en principio parecia funcionar correctamente, pero cuando pasaba a segundo plano, dejaba de funcionar la sincronizacion. Este comportamiento era raro, ya que la actualizacion y documentacion de la libreria no indicaba la necesidad de ningun cambio para la nueva version.

Al volver a realizar las pruebas con la aplicacion en segundo plano, encontramos que estaba fallando con un mensaje de permisos insuficientes.

Esto sucedia debido a que iOS a partir de su version 15, necesita de un nuevo entitlement para acceder a la informacion de salud en segundo plano.

Luego de agregar **com.apple.developer.healthkit.background-delivery** a la lista de entitlements, todo comenzo a funcionar correctamente.

<figure class="wp-block-image size-full">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/08/healthkit_0.jpg?resize=782%2C208&ssl=1)</figure>## Referencias

[https://developer.apple.com/documentation/bundleresources/entitlements/com\_apple\_developer\_healthkit\_background-delivery](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_healthkit_background-delivery)