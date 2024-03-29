---
title: Create the Directory Structure
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


First, create the directory structure in which we hold the website data to the serve on the internet for the visitors.

The Default Document Root location is `/var/www/`. Apache always looks at `/var/www/` to find the content of the site. If you want to change the default path of Document Root. Simply edit the main Apache configuration file `/etc/httpd/conf/httpd.conf`.

To change the Document root edit the configuration file and the change the path of `Document Root` and the `Directory` of the `Document Root`.

Create the Directories using the `mkdir` command with `-p` extension that allow us to create a folder with a nested folder inside it.

In these directories we will create the `public_html` that hold our actual website files. It's not compulsory that you have to put the files `public_html` folder.

If you want to host multiple website then you have to create multiple directories for each of the Domain.

```shell
mkdir -p /var/www/securezone.co.za/public_html
mkdir -p /var/www/api.securezone.co.za/public_html
```
