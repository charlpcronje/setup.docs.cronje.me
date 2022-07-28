---
title: Install Cloud9
label: Install Cloud9 IDE
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


`Cloud9` is a complete web based IDE with terminal access. This container is for running their core SDK locally and developing plugins.

## Supported Architectures

Our images support multiple architectures such as x86-64, arm64 and armhf. We utilise the docker manifest for multi-platform awareness. More information is available from docker here and our announcement here.
Simply pulling lscr.io/linuxserver/cloud9 should retrieve the correct image for your arch, but you can also pull specific arch images via tags.

The architectures supported by this image are

| Architecture          | Tag
|-----------------------|----------------|
| x86-64                | amd64-latest   |
| arm64                 | arm64v8-latest |
| armhf                 | arm32v7-lates  |

## Version Tags

This image provides various versions that are available via tags. latest tag usually provides the latest stable version. Others are considered under development and caution must be exercised when using them.

| Tag         | Description                                         |
|-------------|-----------------------------------------------------|
| latest      | Docker and Compose environment pre-installed        |
| go          | Basic Golang environment pre-installed              |
| nodejs      | Current stable NodeJS/NPM environment pre-installed |
| python      | Current Python3 environment pre-installed           |
| ruby        | Current Ruby environment pre-installed              |

## Application Setup

Access the webui at [http://your-ip:5555](http://your-ip:5555),

## Usage

To help you get started creating a container from this image you can either use docker-compose or the docker cli

```yml
---
version: "2.1"
services:
  cloud9:
    image: lscr.io/linuxserver/cloud9
    container_name: cloud9
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - GITURL=https://github.com/linuxserver/docker-cloud9.git
      - USERNAME=cp
      - PASSWORD=changeme
    volumes:
      - /var/www:/code
      - /var/run/docker.sock:/var/run/docker.sock
    ports:
      - "104.192.7.185:5555:8000"
    restart: unless-stopped
```

## Parameters

Docker images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>`:`<internal>` respectively. For example, `-p 8080:80` would expose `port 80` from inside the container to be accessible from the host's IP on `port 8080` outside the container

### Ports (-p)

| Parameter     | Function                              |
|---------------|---------------------------------------|
| 8000          | The port for the Cloud9 web interface |

Environment Variables (-e)
| Env                                                        | Function                                         |
|------------------------------------------------------------|--------------------------------------------------|
| PUID=1000                                                  | for UserID - see below for explanation           |
| PGID=1000                                                  | for GroupID - see below for explanation          |
| TZ=Europe/London                                           | Specify a timezone to use EG Europe/London       |
| GITURL=`https://github.com/linuxserver/docker-cloud9.git`  | Specify a git repo to checkout on first startup  |
| USERNAME=                                                  | Optionally specify a username for http auth      |
| PASSWORD=                                                  | Optionally specify a password for http auth      |

> if USERNAME and PASSWORD are not set, there will be no http auth

## Volume Mappings (-v)

| Volume               |  Function                                                                          |
|----------------------|------------------------------------------------------------------------------------|
| /code                |  Optionally if you want to mount up a local folder of code instead of checking out |
| /var/run/docker.sock |  Needed if you plan to use Docker or compose commands                              |

## Environment variables from files (Docker secrets)

You can set any environment variable from a file by using a special prepend FILE__.
As an example:
-e FILE__PASSWORD=/run/secrets/mysecretpassword
