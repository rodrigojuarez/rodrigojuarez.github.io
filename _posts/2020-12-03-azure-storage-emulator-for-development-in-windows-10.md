---
id: 57
title: 'Azure Storage emulator for development in Windows 10'
date: '2020-12-03T10:22:49-03:00'
author: 'Rodrigo Juarez'
layout: post
guid: 'http://blog.rodrigojuarez.com/?p=57'
permalink: /2020/12/03/azure-storage-emulator-for-development-in-windows-10/
jabber_published:
    - '1607001769'
timeline_notification:
    - '1607001769'
publicize_linkedin_url:
    - null
publicize_twitter_user:
    - rodrigojuarez
categories:
    - Azure
    - Backend
    - Docker
---

I want to be able to run locally my back end apps that use Azure while I’m working on it.

In the past I used the Azure Storage Emulator but is no longer being supported, [Azurite](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azurite) is the new version and in this post I will show you how to install it and start using it.

## Install

There are several ways to install Azurite in your development machine like a Visual Studio Code extension, NPM or Docker, we are going to use Docker (If you don’t have it installed, check my post [Installing Docker for Windows](http://blog.rodrigojuarez.com/2020/12/02/installing-docker-for-windows-10/)).

Open a powershell command prompt and use the following command to pull the latest Azurite docker image

```
<pre class="wp-block-syntaxhighlighter-code">docker pull mcr.microsoft.com/azure-storage/azurite
```

## Run

Run Azurite with the following powershell commands

```
<pre class="wp-block-code">```
`md c:\azurite`

docker run -p 10000:10000 -p 10001:10001 -v c:/azurite:/data mcr.microsoft.com/azure-storage/azurite
```
```

Now Azurite is ready to be used and you can use your Azure Storage Explorer to access your data or develop your apps.

## References

[Azurite](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azurite?toc=/azure/storage/blobs/toc.json)