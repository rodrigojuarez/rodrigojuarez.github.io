---
id: 61
title: 'Installing Docker for Windows 10'
date: '2020-12-02T10:58:10-03:00'
author: 'Rodrigo Juarez'
layout: post
guid: 'http://blog.rodrigojuarez.com/?p=61'
permalink: /2020/12/02/installing-docker-for-windows-10/
jabber_published:
    - '1606917490'
timeline_notification:
    - '1606917491'
publicize_linkedin_url:
    - null
publicize_twitter_user:
    - rodrigojuarez
categories:
    - Docker
tags:
    - Docker
    - Virtualization
---

Docker Desktop for Windows is Docker for Windows 10, you can get the installer from [here](https://hub.docker.com/editions/community/docker-ce-desktop-windows/).

I started the installer, and continue using the default options.

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2020/12/image.png?resize=706%2C489&ssl=1)</figure>After the installation is completed (reboot required), I needed to download and [install the WSL 2 Linux Kernel](https://aka.ms/wsl2kernel) and reboot again.

One of the advantages of using WSL is that we can now run Hyper-V (I use Hyper-V for android emulators) side by side with Linux containers, this was not possible before when Docker needed to use VirtualBox.

At this point Docker is installed and we can follow the provided tutorial.

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2020/12/image-1.png?resize=782%2C450&ssl=1)</figure>To check that everything is working as expected, we can open a powershell window and execute the *docker -v* command.

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2020/12/image-3.png?resize=671%2C299&ssl=1)</figure>Also in the context menu from the docker taskbar icon, we can switch to Windows Containers

<figure class="wp-block-image size-large">![](https://i0.wp.com/blog.rodrigojuarez.com/wp-content/uploads/2020/12/image-4.png?resize=331%2C390&ssl=1)</figure>And that is all! I hope this was useful and let me know what do you think in the comments!