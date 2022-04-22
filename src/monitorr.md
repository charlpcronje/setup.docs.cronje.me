# Monitor Dashboard

I'm running this dashboard in a container

- Open Portainer
- Add Container
- Name: monitorr/monitorr
- Click on `Publish a new network port`
  - Host Port: 4445
  - Container Port: 80
- Add the `env` variables
  - PUID: 1000
  - PGID: 1000
  - TZ: Africa/Johannesburg
- Click on Deploy container  
- Go to [http://yourserver:4445](http://yourserver:4445)