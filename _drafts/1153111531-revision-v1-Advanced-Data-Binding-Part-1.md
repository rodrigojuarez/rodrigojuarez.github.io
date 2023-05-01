---
id: 11534
title: 'Advanced Data Binding Part 1'
date: '2021-12-30T13:14:04-03:00'
author: 'Rodrigo Juarez'
layout: revision
guid: 'https://blog.rodrigojuarez.com/?p=11534'
permalink: '/?p=11534'
---

This is the first in a series on **advanced data binding**. In this series we will look at: using value converters with binding, relative binding, the {Binding .} and {Binding self} constructs, and more.

We hope to release one of these every week or two.

##  Getting Started

We will be posting Part 0 shortly.

## Samples 

For each topic we discuss, we will provide a simple sample (as simple as possible but no simpler) which we’ll put up on Github and we’ll provide the URL in the blog post. We will walk through that sample to eliminate any confusion and to drive home what we’ve said about the topic.

Some of the samples we’ll make up for this series, others we’ll steal from the Microsoft documents. Which reminds me, why would you read this instead of the official documents? The answer, for me, is that the Microsoft documents are very thorough, but sometimes that can be overwhelming. Most important, however is that triangulating from multiple sources can help zero in on a full understanding.

## Topic #1: Paths

The use of the path keyword is a good, intermediate place to start. It can be used in a number of ways. The most frequent is either to point to a property of an object held in a resource, or to point to a property of a property.

## Example

Here is an example we can take apart. To create this example, I opened VS22 and created a new cross platform (Xamarin.Forms) application. This gave me MainPage.xaml and MainPage.xaml.cs which for this simple example is all we need.

I will leave MainPage.xaml.cs alone, and do all the work in MainPage.xaml. All of the use of path in this example will be declarative.

Here is the complete example:

```
<pre class="wp-block-code">```
<ContentPage
	x:Class="PathDemo.MainPage"
	xmlns="http://xamarin.com/schemas/2014/forms"
	xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
	xmlns:globe="clr-namespace:System.Globalization;assembly=netstandard"
	x:Name="page">

	<StackLayout Margin="10,50">

		<TimePicker x:Name="timePicker" Time="17:05" />

		<Label Text="{Binding Source={x:Reference timePicker}, Path=Time.TotalSeconds, StringFormat='{0} total seconds'}" />

		<Slider
			x:Name="slider"
			BackgroundColor="DarkSlateGray"
			Maximum="10"
			Minimum="0"
			ThumbColor="Red"
			Value="4" />

		<!--  Path and BindingContext set in the binding  -->
		<Label Text="{Binding Source={x:Reference slider}, Path=Value, StringFormat='The value of slider is {0}'}" />

		<!--  Path as content property  -->
		<Label Text="{Binding Value, Source={x:Reference slider}, StringFormat='The value of slider is {0}'}" />

		<!--  Path as content property & setting the binding context  -->
		<Label BindingContext="{x:Reference slider}" Text="{Binding Value, StringFormat='The value of slider is {0}'}" />

		<Label Text="{Binding Source={x:Static globe:CultureInfo.CurrentCulture}, Path=DateTimeFormat.DayNames[3], StringFormat='The middle day of the week is {0}'}" />

	</StackLayout>

</ContentPage>

```
```

The first step is to declare a TimePicker control named timePicker (the name will be important). We initialize its time to 17:05 (5:05pm).

We are now ready to access a property the TimePicker control, Time. But we don’t want that property, we want the subproperty TotalSeconds. No problem, we set the source to the TimePicker as a Reference using the name (timePicker) and then set the path to the subproperty we are interested in. We can then make use of the StringFormat clause to display the total seconds

In the second part of this example,we declare a slider, and set a few attributes, including initializing its value to 4. We are now ready to access the slider and its value. If you have setup INotifyPropertyChanged, as you move the slider the value in the Label will be updated.

Notice that in the next part (Path as Content Property) we bind to the Value and then provide the source, and do not have to make the implied path explicit. That is, we could write

```
<pre class="wp-block-code">```
<!--  Path as content property  -->
<Label Text="{Binding Path=Value, Source={x:Reference slider}, StringFormat='The value of slider is {0}'}" />

```
```

But in this case, the path is redundant.

We then see the option to set the BindingContext explicitly to the slider, and then we can continue to bind to the value .

The short story here is that there are a number of ways to set the (implicit or explicit) binding context (see Post 0)

In the final part of this example, we bind to the CurrentCulture which allows u to use an indexed path. Study this one a bit, it is not intuitive that you can do this.

Future posts will be a bit more complex and/or advanced, but we wanted to start out easy.

Additional documentation about binding path can be found [here](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/binding-path).

The source code for this example (and all examples in this series) can be found [here](https://github.com/XamEsp/XFDataBinding).

This blog post and sample was written (as all will be) by Rodrigo Juarez and Jesse Liberty. Watch for a Spanish translation soon.

Rodrigo Juarez is a full-stack and Xamarin Certified Mobile Professional developer. His mission is to solve complex problems for his clients focusing on the results, applying the most adequate technology available and best practices to ensure a cost-effective and high-quality solution. He has 20+ years of experience in a wide variety of projects in the development of applications for web, desktop and mobile using Microsoft technologies in areas such as management, services, insurance, pharmacy and banks. He can be reached at [**Rodrigo Juarez**](http://www.rodrigojuarez.com/)