# Double Commander Install

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
