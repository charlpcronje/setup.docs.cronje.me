---
title: Let's Encrypt Free Wildcard SSL Certificate
label: Let's Encrypt Free Wildcard SSL Certificate
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


## Via NginX Proxy Manager

Here is the problem I'm facing... I want to have multi-level sub-domains for examele

*.docs.CRONje.ME

I would have thought a wildcard certificate for CRONje.ME would be sufficient, but it is not. A wildcard certificate for CRONje.ME only covers `*.CRONje.ME` and not for `*.docs.CRONje.ME`

So to get past this problem I need more wildcard certificates and I don't want to pay for them. So this is how:

- The easiest way is to install [NginX Proxy Manager](https://setup.docs.CRONje.ME/nginxproxymanager)
- From there you can click on Add Proxy Host
- On The SSL tab, Select request SSL Certificat
- Either complete DNS Challenge or enter email address. But you can't request a wildcard certificat without DNS Chanllenge and my host `ionos.com` don't give out API keys for free

## Via Acme PHP

Acme PHP is available as a single PHAR file to download on Github. For security purposes, this PHAR file is signed using OpenSSL to ensure you are using a valid Acme PHP binary.

[Acme PHP Setup](acmephp.md)
