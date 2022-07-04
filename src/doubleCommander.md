---
title: Double Commander Install
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


Double Commander is a free cross platform open source file manager with two panels side by side. It is inspired by Total Commander and features some new ideas.

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
  doublecommander:
    image: lscr.io/linuxserver/doublecommander
    container_name: doublecommander
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Africa/Johannesburg
    volumes:
      # Enter your config path below after the - and before the :
      - /var/www/tools/doubleCommander/config:/config
      # Enter your data path below after the - and before the :
      - /var/www/tools/doubleCommander/data:/data
    ports:
      - 4448:3000
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

[http://yourhost:3000/](http://yourhost:3000/)
By default the user/pass is abc/abc, if you change your password or want to login manually to the GUI session for any reason use the following link:

[http://yourhost:3000/?login=true](http://yourhost:3000/?login=true)
