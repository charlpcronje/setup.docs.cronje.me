---
title: Install Cockpit on CentOS 7
label: Install Cockpit on CentOS 7
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


## Installation

```shell
sudo yum install cockpit
```

## Enable cockpit

```shell
sudo systemctl enable --now cockpit.socket
```

## Open the firewall if necessary

```shell
sudo firewall-cmd --permanent --zone=public --add-service=cockpit
sudo firewall-cmd --reload
```

## Make Cockpit proxy aware

To make cockpit proxy aware so that you can run it via NginX Reverse Proxy you need to do the following

For security Cockpit will be unable to serve requests from origins it is unfamiliar with due to cross domain limitations. In our example, Cockpit will see the origin as cockpit.domain.tld however it will believe it's running on `127.0.0.1` and therefore be unable to serve the request.

To make Cockpit proxy aware, you will need to modify the Cockpit config file located at `/etc/cockpit/cockpit.conf`. This file may not exist and if it doesn't you should create it.

```conf
[WebService]
Origins = https://cockpit.CRONje.ME wss://cockpit.CRONje.ME
ProtocolHeader = X-Forwarded-Proto
```

These changes will let Cockpit know that connections will come through for https (secure http) and wss (secure websockets) on the subdomain cockpit.domain.tld, and that it should look for the X-Forwarded-Proto header to determine if the connection is secure or not, this is important as Cockpit will redirect any non-local connection from http to https automatically and sees cockpit.domain.tld is non-local.

Once these changes are made you will need to restart cockpit.

## Error ERR_TOO_MANY_REDIRECTS

proxy_pass `http://127.0.0.1:9090`; to proxy_pass `https://127.0.0.1:9090`;

So in your NginX Proxy Manger, set the `Scheme` to `https`
