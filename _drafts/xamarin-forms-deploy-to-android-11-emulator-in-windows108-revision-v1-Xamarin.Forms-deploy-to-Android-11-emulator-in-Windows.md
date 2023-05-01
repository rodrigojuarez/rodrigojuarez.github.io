---
id: 115
title: 'Xamarin.Forms deploy to Android 11 emulator in Windows'
date: '2021-02-25T11:40:20-03:00'
author: 'Rodrigo Juarez'
layout: revision
guid: 'https://blog.rodrigojuarez.com/?p=115'
permalink: '/?p=115'
---

I’m usually using the Android emulator while I’m working with VS, and today I was trying to build and deploy to a newly created Android 11 emulator with no luck.

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2021/02/image.png?resize=782%2C316&ssl=1)</figure>As always, Stack Overflow to the rescue!

In [this link](https://stackoverflow.com/questions/63530855/xamarin-app-cant-deploy-to-android-11-emulator), they comment that the problem is that with Android 11 we need a different way of sign the apk.

I didn’t found the option to do it using the UI, so, we need to add the following tag to our Android csproj file for the debug configuration.

```
<pre class="wp-block-code">```
<AndroidUseApkSigner>true</AndroidUseApkSigner>
```
```

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2021/02/image-1.png?resize=782%2C185&ssl=1)</figure>I also needed to disable the use of Shared Runtime and Fast Deployment in the Android project properties

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2021/02/image-2.png?resize=720%2C242&ssl=1)</figure>After all the changes, my app is deploying to the Android 11 emulator without issues!