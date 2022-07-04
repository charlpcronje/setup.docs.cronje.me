---
title: Install Dash Machine
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


Dash Machine is another app dashboard, it looks to have a few features, but we'll see afthe install

This is my own docker compose file, they project does not have an offical compose file

## Via Portainer

- I'm using portainer to create my stacks from thes Docker Compose Yaml files
- Open Portaier
- Click on Stacks
- New Stack
- Give it name
- Paste the folling in the Docker Composer field

## Docker Composer Script

```yml
services:

  dashmachine:
    container_name: dashmachine
    hostname: dm.CRONje.ME
    image: rmountjoy/dashmachine
    logging:
      driver: json-file
      options:
        max-size: 50m
    ports:
      - 5005:5000
    restart: unless-stopped
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /var/www/tools/dashmachine/userdata:/DashMachine/dashmachine/user_data
      - /var/www/tools/dashmachine/storage:/storage
```

## Default User

`User`: admin
`Password`: admin

Click on add Stack

Done!
