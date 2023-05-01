---
id: 116
title: 'External access to your API in development with Conveyor'
date: '2021-03-06T15:11:50-03:00'
author: 'Rodrigo Juarez'
layout: post
guid: 'https://blog.rodrigojuarez.com/?p=116'
permalink: /2021/03/06/external-access-to-your-api-in-development-with-conveyor/
jabber_published:
    - '1615054310'
timeline_notification:
    - '1615054311'
publicize_twitter_user:
    - rodrigojuarez
publicize_linkedin_url:
    - null
image: /wp-content/uploads/2021/03/pexels-kindel-media-7054501.jpg
categories:
    - Backend
tags:
    - API
    - Conveyor
    - 'Visual Studio'
    - Xamarin
---

In my usual workflow, when I’m developing an API with Visual Studio, and I need to access it from a mobile app, I publish the API to Azure or a local IIS server.  
I need to do this because, by default, IIS express publish your API with the localhost endpoint, and it can’t be easily used outside the running machine.  
I was looking for a quick fix when I found [Conveyor, a Visual Studio extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-1448185.ConveyorbyKeyoti) that automatically provides our API’s external access. Additionally, I created an account on their website to enable public access to my API (outside of the local network).  
After installing the extension, it would start when I run my project in Debug mode.  
In the following screenshot, you can see which ones are the enabled endpoints.

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2021/03/conveyor_endpoints.png?resize=782%2C253&ssl=1)<figcaption>Enabled endpoints</figcaption></figure>  
We can also enable the use of certificates for HTTPS access.  
A great addition to my toolbox, easy to install and use 😉