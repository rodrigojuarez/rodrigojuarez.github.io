---
id: 121
title: 'Json formatting for debug using powershell, jq and Visual Studio Code'
date: '2021-05-10T13:52:51-03:00'
author: 'Rodrigo Juarez'
layout: post
permalink: /2021/05/10/json-formatting-for-debug-using-powershell-jq-and-visual-studio-code/
image: /wp-content/uploads/2021/05/analytics-3088958_1920.jpg
categories:
    - Development
tags:
    - Debugging
    - Development
    - JSON
---

When I’m debugging applications, I usually need to check some JSON responses.

If you only want to see the formatted JSON, you can use [jq](https://stedolan.github.io/jq/download/) with PowerShell (BTW I installed jq [using chocolatey](https://dev.to/codingcoach/chocolatey-a-better-way-to-install-software-on-windows-ljo)), running the following PowerShell command in your terminal:

```
get-clipboard|jq
```

![](/wp-content/uploads/2021/05/get-clipboard-result.png?resize=401%2C266&ssl=1)But usually, I have a considerable chunk of JSON data, and I want to be able to interact with the tree and collapse it.

To do that, I can create a PowerShell script with the following snippet and save it in a folder included in my path and then call it from a PowerShell prompt after copying the JSON to the clipboard.

```
$clipboardFile = "$env:TEMP\clipboard.json"
get-clipboard > $clipboardFile|code $clipboardFile
```

For example, I created the file jtoc.ps1 in my c:\\windows folder, and I can copy the following JSON to the clipboard `{"Hello":"json formatter","Using":"vs code"}` and then use `jtoc` in the terminal and it will open in vs code, then I use ALT+SHIFT+F to format the text.

![](/wp-content/uploads/2021/05/json-formatted.png?resize=757%2C178&ssl=1)I hope this was useful and a better way to check your JSON data.