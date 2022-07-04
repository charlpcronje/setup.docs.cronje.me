---
title: Install CWP Control Panel
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

DO NOT INSTALL

> Okay so this did sound like a good idea, but it is a very bad one. Once you have installed CWP you lose manual
> control of a lot of systems and you can not uninstall the damn thing, it is a piece of shit. The only way to remove this piece of crap is to reinstall your entire OS... Damn Why don't they warm you before you start

## Quick Into

- This control panel is a lot like CPanel, you can manage the following within the panel
  - Web
  - Email
  - Users
  - Domains
  - Firewall
  - Database

I've now been trying for a while to run two version of php at the same time, but all the tutorial fall over at some stage. so I decided to rather get a tool that has this functionally built in to have specific PHP versions for each vHost

## Install CWP

```shell
yum -y install wget
yum -y update
reboot
cd /usr/local/src
wget https://centos-webpanel.com/cwp-el7-latest
sh cwp-el7-latest
```
