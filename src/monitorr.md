---
title: Monitor Dashboard
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

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