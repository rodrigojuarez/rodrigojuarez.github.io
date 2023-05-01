---
id: 11561
title: 'Advanced Databinding Part 2: Converters'
date: '2022-01-13T15:54:08-03:00'
author: 'Rodrigo Juarez'
layout: revision
guid: 'https://blog.rodrigojuarez.com/?p=11561'
permalink: '/?p=11561'
---

There are times when you need to bind to a source but the source is not in the right format or otherwise needs to be manipulated.

For example, suppose, as we’ll show below, that you have a text entry and a button, but you only want the button enabled as long as there are one or more characters in the text entry, and of course if there is no text entered you want to disable button.

You could bind the button to a boolean property in your View Model and bind the text to another property and then on text changed you could test to see if there is text in the entry control and update the button. Yuck.

# Value Converters

For example, since “IsEnabled takes a boolean and the number of characters is an int, you need a way to convert that int into a bool. That is where value converters enter the picture.

The standard format for a value converter is

- Implement IValueConverter
- Implement a method Convert according to the interface
- Implement a method ConvertBack according to the interface

Note that frequently you won’t need ConvertBack. In that case, implement it to return null or to throw a NotImplemented exception.

Our converter is pretty common. Since we want to convert an int to a bool, we’ll use the clever name IntToBoolConverter.

Next, we implement the first method, Convert

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

And for ConvertBack we’re going to say if the value is true, return 1 otherwise return 0

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

# Using the Converter

Our test code is as simple as can be. We have an entry which has no text in it, and a button whose IsEnabled value depends on binding to that control, but converting the int (how many characters) to a bool (enable or not).

We start by creating a ResourceDictionary, in this case at the top of the XAML page (which is very common for resources you are only going to use on one page)

```
<pre class="wp-block-code">```
<ContentPage.Resources>
	<ResourceDictionary>
		<local:IntToBoolConverter x:Key="intToBool" />
	</ResourceDictionary>
</ContentPage.Resources>


```
```

Note: For resources you are going to use on many pages, you will want to put the resource in a ResourceDictionary in app.xaml. You will access it in exactly the same way as all the ResourceDictionaries in a project are merged at compile time.

Notice that we’ve assigned a key to the converter, this allows us to use the key in the XAML.

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

The Entry does not know about the converter, but the button does: specifically its IsEnabled property binds to the Entry (by name) and sets the Path to the text.length (how many characters). For more on Binding Paths, please see Part 1 of this series: [Paths](https://jesseliberty.com/2021/12/29/11531/).

Finally the IsEnabled binding invokes the converter. This will pass in the number of characters and if it is not zero it will return true (and enable the button), otherwise it will return false (and disable the button).

That’s all there is to it.

Note that this particular converter is so common that it is provided as part of the Xamarin Community Toolkit, which along with dozens of other very useful things, provides a number of common converters such as EnumToIntConverter, InvertedBoolConverter (change false to true and vice versa) and many others. You can find the Xamarin Community Toolkit [here](https://docs.microsoft.com/en-us/xamarin/community-toolkit/)

Find out more about converters in the Microsoft Docs, [here](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/converters)

Rodrigo Juarez is a full-stack and Xamarin Certified Mobile Professional developer. His mission is to solve complex problems for his clients focusing on the results, applying the most adequate technology available and best practices to ensure a cost-effective and high-quality solution. He has 20+ years of experience in a wide variety of projects in the development of applications for web, desktop and mobile using Microsoft technologies in areas such as management, services, insurance, pharmacy and banks. He can be reached at [**Rodrigo Juarez**](http://www.rodrigojuarez.com/)

Note, this is the 1,300th post on this site!

.