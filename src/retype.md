---
title: Retype Install
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

Retype is an ✨ ultra-high-performance ✨ generator that builds a website based on simple text files. Focus on your writing while Retype builds the rest.

## Install via NPM

```shell
npm install retypeapp --global
retype watch
```

## Basic Usage

I recommend the following:

- When you have a bunch of markdown files in a folder you want to create a wiki from, then create two folders in side the current root folder of the markdown folders

```shell
# Lets say the files are in /var/www/docs
mkdir /var/www/temp
mv /var/www/docs/* /var/www/temp/
mkdir /var/www/docs/src
mkdir /var/www/docs/public
mv var/www/temp/* /var/www/docs/src/
cd /var/www/docs
retype init
```

Now all the files are in `/var/www/docs/src` and you will have `retype.yml` file in `/var/www/docs`

Open `retype.yml`

```yml
#Your file content should be updated to look something like
input: src                    # Where Retype will look for the files to generate site from
output: public                # The destination where it must create the website
url: http://docs.CRONje.ME   # Optional, this is where the site will be hosted
branding:
  title: Dev Serv Docs
  label: Docs
links:                        # Here you can add as many links as you want, repeating the -text, link
- text: Getting Started
  link: http://docs.CRONje.ME/gettingStarted/
footer:
  copyright: "webAlly &copy; Copyright {{ year }}. All rights reserved."
```
