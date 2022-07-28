---
title: ACME PHP
label: ACME PHP Install
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


Acme PHP is available as a single PHAR file to download on Github. For security purposes, this PHAR file is signed using OpenSSL to ensure you are using a valid Acme PHP binary.

## Install ACME PHP

Check the latest stabel release from: [https://github.com/acmephp/acmephp/releases](https://github.com/acmephp/acmephp/releases)

Run following commands:

```sh
cd ~
php -r "copy('https://github.com/acmephp/acmephp/releases/download/2.0.0/acmephp.phar', 'acmephp.phar');"
php -r "copy('https://github.com/acmephp/acmephp/releases/download/2.0.0/acmephp.phar.pubkey', 'acmephp.phar.pubkey');"
```

Get the AcmePHP Version

```sh
php acmephp.phar --version
```

If the last command display the Acme PHP version, you are ready to use Acme PHP.

- Use the latest development version
- While we strongly recommand you to use a stable (or at least pre-release) version, you can also use the latest development build if you need the latest features.

You can install it by running the following commands:

```sh
cd ~
php -r "copy('https://acmephp.github.io/downloads/acmephp.phar', 'acmephp.phar');"
php -r "copy('https://acmephp.github.io/downloads/acmephp.phar.pubkey', 'acmephp.phar.pubkey');"
```

Get the AcmePHP Version

```sh
php acmephp.phar --version
```
