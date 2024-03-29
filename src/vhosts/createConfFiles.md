---
title: Create New Virtual Host Conf Files
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


[_Back to Index_](../README.md)

Create `.conf` files in `/etc/httpd/conf.d`

```shell
#IMPORTANT Main domains and sub-domains go in the same .conf file
nano /etc/httpd/conf.d/securezone.co.za.conf
```

Add the following in the conf file for both sub and main domain

```conf
<VirtualHost *>
    ServerName securezone.co.za
    ServerAlias www.securezone.co.za
    ServerAdmin charl@isa.co.za
    DocumentRoot /var/www/securezone.co.za/public_html

    <Directory /var/www/securezone.co.za/public_html>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/www/securezone.co.za/error.log
    CustomLog /var/www/securezone.co.za/access.log combined
</VirtualHost>

<VirtualHost *>
    ServerName api.securezone.co.za
    ServerAlias securezone.co.za
    ServerAdmin charl@isa.co.za
    DocumentRoot /var/www/api.securezone.co.za/public_html/public

    <Directory /var/www/api.securezone.co.za/public_html/public>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>
    ErrorLog /var/www/api.securezone.co.za/error.log
    CustomLog /var/www/api.securezone.co.za/access.log combined
</VirtualHost>
```

I also setup the website Philip Made

```conf
<VirtualHost *>
    ServerName old.securezone.co.za
    ServerAlias securezone.co.za
    ServerAdmin charl@isa.co.za
    DocumentRoot /var/www/old.securezone.co.za/public_html/public

    <Directory /var/www/old.securezone.co.za/public_html/public>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>
    ErrorLog /var/www/old.securezone.co.za/error.log
    CustomLog /var/www/old.securezone.co.za/access.log combined
</VirtualHost>
```

And a demo site for graphQL with a graphQL Playground

```conf
<VirtualHost *>
    ServerName graph.securezone.co.za
    ServerAlias securezone.co.za
    ServerAdmin charl@isa.co.za
    DocumentRoot /var/www/graph.securezone.co.za/public_html/public

    <Directory /var/www/graph.securezone.co.za/public_html/public>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>
    ErrorLog /var/www/graph.securezone.co.za/error.log
    CustomLog /var/www/graph.securezone.co.za/access.log combined
</VirtualHost>
```

Added Assets sub-domain for some assets and the theme

```conf
<VirtualHost *>
    ServerName assets.securezone.co.za
    ServerAlias securezone.co.za
    ServerAdmin charl@isa.co.za
    DocumentRoot /var/www/assets.securezone.co.za/public_html

    <Directory /var/www/assets.securezone.co.za/public_html>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/www/assets.securezone.co.za/error.log
    CustomLog /var/www/assets.securezone.co.za/access.log combined
</VirtualHost>
```

Added Vite VueJs and Quasar App

```conf
<VirtualHost *>
    ServerName vue.securezone.co.za
    ServerAlias securezone.co.za
    ServerAdmin charl@isa.co.za
    DocumentRoot /var/www/vue.securezone.co.za/public_html

    <Directory /var/www/vue.securezone.co.za/public_html>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/www/vue.securezone.co.za/error.log
    CustomLog /var/www/vue.securezone.co.za/access.log combined
</VirtualHost>
```

Restart httpd

```shell
systemctl restart httpd
```
