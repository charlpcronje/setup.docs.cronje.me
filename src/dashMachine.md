# Install Dash Machine

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
