---
id: 11560
title: 'Databinding Avanzado Parte 2: Converters'
date: '2022-01-03T10:24:35-03:00'
author: 'Rodrigo Juarez'
layout: post
guid: 'https://jesseliberty.com/?p=11560'
permalink: /2022/01/03/advanced-databinding-part-2-converters/
jabber_published:
    - '1642113504'
timeline_notification:
    - '1642113505'
publicize_twitter_user:
    - rodrigojuarez
image: /wp-content/uploads/2022/01/pexels-photo-270348.jpeg
categories:
    - 'Advanced Data Binding'
    - Essentials
    - Xamarin.Forms
tags:
    - Xamarin
---

En ocasiones, podemos necesitar enlazar a un origen de datos, pero el origen puede no estar en el formato correcto, en esos casos necesitamos manipularlo.

Por ejemplo, supongamos, como veremos a continuacion, que tenemos una caja de texto y un boton, y queremos que el boton se encuentra habilitado solamente cuando la caja de texto tenga uno o mas caracteres.

Podriamos enlazar el boton a una propiedad booleana en el view model y el texto a otra propiedad string, entonces cuando el texto cambia, podemos actualizar la propiedad booleana. Utilizar esta tecnica funciona, pero agrega complejidad innecesaria. Veremos a continuacion una mejor solucion utilizando value converters.

# Value Converters

Ya que la propiedad del boton **IsEnabled** utiliza un valor de tipo booleano y el numero de caracteres es del tipo int, necesitamos una manera de convertir dichos valores. Aqui es donde podemos ver la utilidad de los **Value Converters**.

Para definir uno nuevo, debemos crear una clase que:

- Implemente **IValueConverter**
- Implemente un metodo **Convert** de acuerdo a la interface
- Implemente un metodo **ConvertBack** de acuerdo a la interface

En muchas ocasiones, no necesitamos implementar el metodo **ConvertBack**, si no vamos a realizar la conversion inversa, en cuyo caso el metodo no es nunca llamado y puede retornar null o lanzar una excepcion del tipo **NotImplementedException**.

Nuestro conversor es bastante comun. Debido a que queremos convertir un **int** en un **bool**, usaremos el nombre **IntToBoolConverter** (muy inteligente de nuestra parte).

A continuacion, implementaremos el primer metodo **Convert**

```
<pre class="wp-block-code">```
 public class IntToBoolConverter : IValueConverter
 {
     public object Convert(object value, 
         Type targetType, 
         object parameter, 
         CultureInfo culture)
     {
         return (int)value!=0;
     }

```
```

Y para el **ConvertBack**, si el valor es **true**, devolveremos 1, sino, 0.

```
<pre class="wp-block-code">```
public object ConvertBack(object value,
    Type targetType, 
    object parameter,
    CultureInfo culture)
{
    return (bool)value ? 1 : 0;
}

```
```

# Usando el Converter

Nuestro codigo para probar el converter, es tan simple como puede serlo. Tenemos una caja de texto en blanco, y un boton cuya propiedad **IsEnabled** utiliza el conversor para determinar el numero de caracteres y devolver un **bool**.

Comenzamos creando un **ResourceDictionary**, al inicio de nuestro archivo XAML (lo cual es habitual para recursos que solo van a utilizarse en solo una pagina).

```
<pre class="wp-block-code">```
<ContentPage.Resources>
	<ResourceDictionary>
		<local:IntToBoolConverter x:Key="intToBool" />
	</ResourceDictionary>
</ContentPage.Resources>


```
```

**Nota**: para recursos que se van a utilizar en muchas paginas, se puede colocar el recurso en un diccionario en el archivo **App.xaml**. Luego se puede utilizar de la misma manera, ya que todos los diccionarios se unen en tiempo de compilacion.

Notar que hemos asignado una clave al converter, lo que nos permite referenciarlo en nuestros archivos XAML.

```
<pre class="wp-block-code">```
<Entry
	x:Name="SearchEntry"
	Placeholder="Enter search term"
	Text=""
	VerticalOptions="CenterAndExpand" />

<Button
	HorizontalOptions="Center"
	IsEnabled="{Binding Source={x:Reference SearchEntry},
	Path=Text.Length,
	<strong>Converter={StaticResource intToBool}}"</strong>
	Text="Search"
	VerticalOptions="CenterAndExpand" />


```
```

El control **Entry** no sabe nada del converter, pero el boton si, por medio del enlace a la propiedad **IsEnabled**, utilizando el Path a **Text.Length** (cuantos caracteres tiene el texto). Para mas informacion sobre **Binding Paths**, ver el primer post de esta serie: [Paths](https://blog.rodrigojuarez.com/2021/12/29/11531/).

Finalmente, el enlace invoca al converter. Le envia el numero de caracteres, y si no es cero, devuelve **true** habilitando el boton, sino devuelve **false**, deshabilitandolo.

Este converter en particular es muy utilizado, y es provisto ademas como parte del Xamarin Community Toolkit, en donde podemos encontrar docenas de funciones adicionales, como **EnumToIntConverter**, o **InvertedBoolConverter** (cambiar false a verdadero y vice versa) entre otros. Pueden encontrar mayor informacion [aqui](https://docs.microsoft.com/en-us/xamarin/community-toolkit/).

Tambien pueden encontrar informacion adicional sobre converters en la documentacion oficial de Microsoft, [aqui](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/converters).

El codigo fuente para este ejemplo (y para todos los ejemplos de esta serie) se encuentra [aqui](https://github.com/XamEsp/XFDataBinding).

Este post y los ejemplos fueron escritos por Jesse Liberty y Rodrigo Juarez.

Jesse Liberty tiene tres decadas de experiencia escribiendo y entregando proyectos de software y ha escrito dos docenas de libros y unas cuantas docenas de cursos en Pluralsight y LinkedIn Learning. Ha sido Senior Technical Evangelist en Microsoft, Distinguished Software Engineer en AT&amp;T, VP en Information Services para Citibank y Software Architect en PBS. El es un Xamarin Certified Mobile Developer, Xamarin MVP y Microsoft MVP. Lo podemos encontrar en [Jesse Liberty](https://jesseliberty.com/).