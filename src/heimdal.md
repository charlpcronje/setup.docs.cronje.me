# Heimdal Dashboard

I'm running this dashboard in a container

- Open Portainer
- Add Container
- Name: linuxserver/heimdal
- Click on `Publish a new network port`
  - Host Port: 4440
  - Container Port: 80
- Add the `env` variables
  - PUID: 1000
  - PGID: 1000
  - TZ: Africa/Johannesburg
- Add Volumes
  - Set the folder on your server where you want the container to store it's data
  - Go and create that folder
- Click on Deploy container  
- Go to [http://yourserver:4440](http://yourserver:4440)
