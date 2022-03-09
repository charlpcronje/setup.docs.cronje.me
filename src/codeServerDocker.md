# Code-Server Via Docker Compose

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
      - PASSWORD=4334.4334            # Password to be entered when you open the url
      - SUDO_PASSWORD=4334.4334       # So that VS Can edit you filesystem
      - PROXY_DOMAIN=code.devserv.me 
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
