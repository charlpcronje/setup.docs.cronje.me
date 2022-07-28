---
title: Code-Server via Docker Compose
label: Code-Server via Docker Compose
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


## Docker Compose

- Open `Portainer`
- Click on `Stacks`
- Click on `Add Stack`
- Give it a `name` in the first field
- Create a folder on your server for the config storage,you will need the full path at `Volumes`
- Paste the following in the `Docker Compose` field

```yml
---
version: "2.1"
services:
  code-server:
    image: lscr.io/linuxserver/code-server
    container_name: code-server
    environment:
      # To get your details just run `id` in terminal
      - PUID=1000
      - PGID=1000
      - TZ=Africa/Johannesburg
      - PASSWORD=changeme            # Password to be entered when you open the url
      - SUDO_PASSWORD=changeme       # So that VS Can edit you filesystem
      - PROXY_DOMAIN=code.CRONje.ME 
      - DEFAULT_WORKSPACE=/var/www    # Where on your filesystem shout it be be when you open it
    volumes:
      - /var/www/tools/vscode/config:/config
    ports:
      - 4444:8443
    restart: unless-stopped
```

- Scroll a bit down and click on Add an environment variable
- Add the following 3 environment variables

```conf
# To get uou PUID and PGID, SSH into you server and type 'id'
PUID : 1000
PGID : 1000
TZ   | Africa/Johannesburg
```

Click on `deploy Stack`

## Application Setup

The application can be accessed at:

[http://devserv:4444/](http://devserv:4444/)
