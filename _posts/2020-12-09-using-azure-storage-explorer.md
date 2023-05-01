---
title: 'Using Azure Storage Explorer'
date: '2020-12-09T12:30:00-03:00'
author: 'Rodrigo Juarez'
layout: post
permalink: /2020/12/09/using-azure-storage-explorer/
categories:
    - Azure
    - Backend
---

![](/wp-content/uploads/2020/12/image-8.png?resize=782%2C161&ssl=1)It’s a free tool to access you Azure cloud storage from your desktop computer.

## Install

You can download the installer [here](https://azure.microsoft.com/en-us/features/storage-explorer/).

Run the installer and select to install it only for you, or all users.

![](/wp-content/uploads/2020/12/image-9.png?resize=362%2C271&ssl=1)Then complete the installation with the default values.

## Connection &amp; first run

On the first start, we can select the connection type to our Azure Storage.

![](/wp-content/uploads/2020/12/image-10.png?resize=611%2C618&ssl=1)Then, we can login with our Azure account to access the storage.

![](/wp-content/uploads/2020/12/image-11.png?resize=782%2C524&ssl=1)The services available in our storage account depends on the configuration at creation time.

## Access to local emulator

If we have configured the [local emulator](2020/12/03/azure-storage-emulator-for-development-in-windows-10/) (Azurite), we can connect using the *Open Connect Dialog* icon.

![](/wp-content/uploads/2020/12/image-12.png?resize=439%2C442&ssl=1)And then the *Attach to a local emulator* option.

![](/wp-content/uploads/2020/12/image-13.png?resize=611%2C618&ssl=1)I have my Azurite instance configured with the default values, so I can connect just setting any Display name.

![](/wp-content/uploads/2020/12/image-14.png?resize=611%2C618&ssl=1)After confirmation, we can access our local Azurite in the same way that we can access our Azure storage (remember to run your local emulator).

![](/wp-content/uploads/2020/12/image-15.png?resize=782%2C523&ssl=1)