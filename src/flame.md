---
title: Install Flame Dashboard
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


## Install via Portainer

- Open Portainer
- Click on Stacks
- Add Stack
- Give the stack a name
- Paste the following under Docker Compose

```yml
version: '2.1'

services:
  flame:
    image: pawelmalak/flame:latest
    container_name: flamedashboard
    volumes:
      - /var/www/tools/flame:/app/data #update the path as necessary
      - /var/run/docker.sock:/var/run/docker.sock #don't change this
    ports:
      - 4446:5005 #change the 6006 port as necessary for your setup
    restart: unless-stopped
```

- Click on Deploy
- Done, now you can go to yourserver.com:4446
