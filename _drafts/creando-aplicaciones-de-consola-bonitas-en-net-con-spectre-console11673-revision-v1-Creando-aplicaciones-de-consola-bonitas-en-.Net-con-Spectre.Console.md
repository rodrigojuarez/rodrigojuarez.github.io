---
id: 11693
title: 'Creando aplicaciones de consola bonitas en .Net con Spectre.Console'
date: '2022-08-26T17:56:36-03:00'
author: 'Rodrigo Juarez'
layout: revision
guid: 'https://blog.rodrigojuarez.com/?p=11693'
permalink: '/?p=11693'
---

En varias oportunidades he tenido que crear aplicaciones de consola que van actualizando la pantalla a medida que va pasando el tiempo o sucede algo, termino teniendo cosas como en la siguiente captura de pantalla

<figure class="wp-block-image size-full">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/08/image.png?resize=418%2C538&ssl=1)</figure>Tratando de mejorar esto, podemos reformatear la informacion y utilizar un `Console.Clear();` para repintar la pantalla, lo cual nos da una salida como la siguiente

<figure class="wp-block-image size-full">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/08/image-1.png?resize=335%2C130&ssl=1)</figure>El problema surge cuando es mucha la informacion que queremos presentar y el armado de la pantalla se vuelve rapidamente muy complicado

Para facilitar este proceso, podemos recurrir a [Spectre.Console](https://spectreconsole.net/), que nos permitira crear aplicaciones de consola mucho mas bonitas

## Instalacion

Solo es necesario agregar una referencia al paquete NuGet de Spectre.Console.

<figure class="wp-block-image size-full">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/08/image-2.png?resize=782%2C340&ssl=1)</figure>## Uso

Una de las funcionalidades disponibles es el uso de [Markup](https://spectreconsole.net/markup), el cual permite enviar texto enriquecido a la consola, como puede verse en el siguiente ejemplo

```
<pre class="wp-block-code">```
        string color;
        switch (loadPercentage)
        {
            case > 80:
                color = "red";
                break;
            case > 30:
                color = "yellow";
                break;
            default:
                color = "green";
                break;
        }

        AnsiConsole.Markup($"CPU usage [{color}]{loadPercentage}[/]%");
```
```

<figure class="wp-block-image size-full">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/08/image-3.png?resize=406%2C129&ssl=1)</figure>Tambien podemos crear widgets como una [Table](https://spectreconsole.net/widgets/table) con el siguiente codigo

```
<pre class="wp-block-code">```
        // Create a table
        var table = new Table();

        // Add some columns
        table.AddColumn("Sensor");
        table.AddColumn("Value");

        // Add some rows
        table.AddRow("CPU usage", $"[{color}]{loadPercentage}[/]%");

        // Render the table to the console
        AnsiConsole.Render(table);
```
```

<figure class="wp-block-image size-full">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/08/image-4.png?resize=343%2C196&ssl=1)</figure>Otra funcionalidad muy interesante, son los componentes [Live](https://spectreconsole.net/live/) que nos permiten modificar solo una parte de la informacion mostrada, sin necesidad de reescribir toda la pantalla.

Vemos en el siguiente codigo como usar un [Live-Display](https://spectreconsole.net/live/live-display) con una tabla, y luego usamos el contexto para refrescar la pantalla

```
<pre class="wp-block-code">```
AnsiConsole.Live(computerInfo.Table).Start(ctx =>
{
    do
    {
        while (!Console.KeyAvailable)
        {
            computerInfo.GenerateFormattedOutput();
            ctx?.Refresh();
            Thread.Sleep(1000);
        }

    } while (Console.ReadKey(true).Key != ConsoleKey.Escape);
});
```
```

Dentro de nuestro metodo `GenerateFormattedOutput` actualizaremos la tabla de la siguiente manera

```
<pre class="wp-block-code">```
Table.UpdateCell(0, 1, $"[{color}]{loadPercentage}[/]%");
```
```

## Codigo de ejemplo

Pueden acceder a un proyecto en el siguiente [repositorio de github](https://github.com/trailheadtechnology/SpectreConsoleDemo), en el cual se encuentra un ejemplo completo de la funcionalidad mostrada en este post

## Conclusion

Como pueden ver, es muy sencillo de utilizar, yo aqui solo he mencionado funcionalidad basica, pero en el sitio del proyecto pueden ver todos los casos de uso, y pantallas mostrando gran cantidad de informacion y otros controles

<figure class="wp-block-image size-full">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2022/08/image-5.png?resize=782%2C630&ssl=1)</figure>