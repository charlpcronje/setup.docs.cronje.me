---
title: Setup NginX as Reverse Proxy
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


## Why reverse proxy

I realized that a lot of the web applications I installed and will be installing does not run on port 80 and are not hosted on Apache, So I need a way to control all of this traffic, I need way to use my SSL certificate on all the ports and I need a way to point my sub-domains to a specific port so that I don't have to use `http://CRONje.ME:9000` for portainer but that I can use `portainer.CRONje.ME`.

## Install NginX

If you have not yet installed Nginx then run command

```shell
yum install nginx
```

That should install Nginx, you can now check if the service is running. But if you have Apache running like I do on `port 80` then Nginx server probably failed to start

```shell
systemctl status nginx
```

You may get the following error: `Unit nginx.service could not be found.`

If so run this command:

```shell
systemctl daemon-reload
```

If you still en error, then try stopping Apache server

```shell
sudo systemctl stop httpd
```

## Set Apache to listen on port 8080

```shell
nano /etc/httpd/conf/httpd.conf
```

## Update these lines

```conf
Listen 127.0.0.1:8080
# Listen 80
```

So you comment out `# Listen 80` and above that comment in and change the IP address to `127.0.0.1:8080` and the port number to `8080`

Restart Apache

```shell
systemctl restart httpd
```

## Set Nginx to Run on Apache user

```shell
nano etc/nginx/nginx.conf
# Update this line
user nginx;
# to
user apache;
```

## Update root web folder and server name

```conf
# your server section should look like this
server {
        listen       80;
        listen       [::]:80;
        server_name  CRONje.ME;
        root         /var/www;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
        location = /404.html {
            root         /var/www;
            proxy_pass http://127.0.0.1:8080/;
            proxy_redirect off;
            proxy_set_header Host $http_host;
            proxy_set_header X-Real-IP $remote_addr;
        }

        error_page 404 /404.html;
        location = /40x.html {
        }
    }
```

## Create proxy.conf

```shell
nano /etc/nginx/conf.d/proxy.conf
```

Add the following to the file

```shell
proxy_redirect off;
proxy_set_header Host $http_host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
client_max_body_size 10m;
client_bod_buffer_size 128k;
proxy_connect_timeout 90;
proxy_send_timeout 90;
proxy_read_timeout 90
proxy_buffer_size 4k;
proxy_buffers 4 32k;
proxy_busy_buffers_size 64k;
proxy_temp_file_write_size 64;
```
