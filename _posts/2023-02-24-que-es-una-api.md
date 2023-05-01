---
title: 'Que es una API?'
date: '2023-02-24T12:21:28-03:00'
author: 'Rodrigo Juarez'
layout: post
permalink: /2023/02/24/que-es-una-api/
image: /wp-content/uploads/2023/02/pexels-cong-h-1404819-1568x1046.jpg
categories:
    - Basicos
    - Development
---

Una API, o “Application Programming Interface”, es una forma en que diferentes sistemas pueden comunicarse y compartir información.

Las APIs están diseñadas para proporcionar una interfaz clara y bien definida para que los desarrolladores de software puedan interactuar con un servicio o plataforma en particular. Por lo tanto, cuando un desarrollador crea una aplicación o un sitio web, puede usar una API existente para acceder a datos o funcionalidades específicas en otro sistema sin tener que crear todo desde cero.

Que significa esto en la practica? A continuacion les voy a mostrar un ejemplo de una API que esta disponibles publicamente para que cualquier desarrollador la pueda utilizar y que devuelve informacion de uno de los temas que son la razon de existir de internet, si, acertaron, [una api de gatos](https://thecatapi.com/)!

Y como funciona esta API? Como otras APIs REST, recibe solicitudes por medio de parametros o en [formato JSON](/2023/02/24/que-es-json/) y responde de acuerdo a nuestra consulta con una respuesta tambien en [formato JSON](/2023/02/24/que-es-json/).

La [documentacion de la api](https://developers.thecatapi.com/) nos indica que una solicitud enviada a la siguiente direccion nos devolvera la informacion de 10 gatos al azar <https://api.thecatapi.com/v1/images/search?limit=10>

Para enviar nuestra solicitud, podemos utilizar cualquier cliente HTTP, como Postman (necesita instalacion en tu computadora) o disponible en linea [reqbin.com](https://reqbin.com/)

Se puede ver en la siguiente imagen que luego de colocar la direccion <https://api.thecatapi.com/v1/images/search?limit=10> (1) y presionar el boton Send o Enviar (2) obtenemos la respuesta en formato JSON (3)

![](/wp-content/uploads/2023/02/image.png?resize=782%2C404&ssl=1)La respuesta es un conjunto de imagenes, en las que cada elemento tiene un identificador unico (id) la ubicacion de la imagen en internet (url), y el ancho (width) y alto (height) de la misma.

En esta misma api, si queremos ver todas las razas (breeds) disponibles, podemos realizar una llamada a <https://api.thecatapi.com/v1/breeds>

Podemos entonces ver en la imagen detalles de las razas disponibles en la API, por ejemplo, Siameses, que usa un identificador “siam”

![](/wp-content/uploads/2023/02/image-1.png?resize=782%2C363&ssl=1)Con esta nueva informacion, podemos hacer una nueva llamada, para obtener gatos solo de la raza siames: [https://api.thecatapi.com/v1/images/search?breed\_ids=siam](https://api.thecatapi.com/v1/images/search?breed_ids=siam)

![](/wp-content/uploads/2023/02/image-2.png?resize=782%2C373&ssl=1)Notese que podemos utilizar cualquiera de los valores devueltos como “url” y colocandolo en nuestro navegador de internet, podremos ver la imagen.

![](/wp-content/uploads/2023/02/image-3.png?resize=782%2C668&ssl=1)Tengamos en cuenta que este es un post introductorio y que el verdadero poder de las APIs sera aprovechado cuando podamos procesar y utilizar la respuesta en nuestros propios programas con nuestro lenguaje preferido.

Intencionalmente he dejado de lado muchos temas que seran explicados luego, como REST, verbos, etc.

Gracias por leer!!