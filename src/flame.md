# Install Flame Dashboard

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
