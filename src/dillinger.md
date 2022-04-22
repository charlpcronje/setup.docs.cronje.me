# Install Dillinger

dillinger is a cloud-enabled, mobile-ready, offline-storage, AngularJS powered HTML5 Markdown editor.

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
  dillinger:
    image: lscr.io/linuxserver/dillinger
    container_name: dillinger
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Africa/Johannesburg
    volumes:
      # Enter your config path below after the - and before the :
      - /var/www/tools/dillinger:/config
    ports:
      - 4442:8080
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
