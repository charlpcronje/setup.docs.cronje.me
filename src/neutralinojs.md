---
title: Neutralinojs
label: Server & Software Setup
order: 100
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
edit:
  repo: "https://github.com/charlpcronje/setup.docs.devserv.me/edit/"
  base: /src
  branch: main
  label: Edit on GitHub
editor:
  enabled: false
favicon: favicon.png
links:
- text: Dashboard
  link: https://nav.cronje.me
- text: Blog / Portfolio
  link: https://blog.cronje.me
- text: Wiki, Tips and Docs 
  link: https://docs.cronje.me
- text: My CV
  link: https://cv.cronje.me
- text: LinkedIn
  link: https://www.linkedin.com/in/charlpcronje
- text: GitHub
  link: https://github.com/charlpcronje
- text: Upwork Profile
  link: https://www.upwork.com/freelancers/~01ccb1439024ec9c50
footer:
  copyright: "webAlly &copy; Copyright {{ year }}. All rights reserved."
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>


Neutralinojs is a lightweight and portable desktop application development framework. It lets you develop lightweight cross-platform desktop applications using JavaScript, HTML and CSS. Apps built with Neutralinojs can run on Linux, macOS, Windows, Web, and Chrome. Also, you can extend Neutralinojs with any programming language (via extensions IPC) and use Neutralinojs as a part of any source file (via child processes IPC).

- [Neutralinojs vs Electron vs NW.JS vs `Tauri` vs `NodeGui` vs `Flutter` vs `.Net MAUI`](https://github.com/Elanis/web-to-desktop-framework-comparison)
[Neutralinojs vs Electron vs NW.js (2018)](https://github.com/neutralinojs/evaluation)
[Roadmap for 2022](https://github.com/neutralinojs/roadmap#roadmap-2022)

## Get started with the neu CLI

## Creating a new app

``` shell
 npm i -g @neutralinojs/neu
 neu create hello-world
 cd hello-world
 neu run
``` 

## Building your app (No compilation - takes less than a second)

```shell
neu build
```

Start building apps: neutralino.js.org/docs

## Why Neutralinojs?

In Electron and NWjs, you have to install `NodeJs` and hundreds of dependency libraries. Embedded Chromium and `Node` make simple apps `bloaty`. Neutralinojs offers a lightweight and portable SDK which is an alternative for Electron and NW.js. Neutralinojs doesn't bundle Chromium and uses the existing web browser library in the operating system (Eg: gtk-webkit2 on Linux). Neutralinojs implements a WebSocket connection for native operations and embeds a static web server to serve the web content. Also, it offers a built-in JavaScript client library for developers.

Ask questions on StackOverflow using tag `neutralinojs`
