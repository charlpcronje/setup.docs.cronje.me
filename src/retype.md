---
title: Retype Install
label: Retype Install
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
