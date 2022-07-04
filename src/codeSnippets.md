---
title: Install Code Snippets
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

Just to demonstrate, I will install this with Docker but not Via Portainer

Just run the following command via SSH

```bash
docker run -d --name snippetbox -p 4447:5000 -v /var/www/tools/snippetBox:/app/data pawelmalak/snippet-box
```

- Sometimes when it is a simple `Docker` setup then it's easier to just do this via `SSH` than to do all the effort to login to `Portainer`
- It does not matter oif you add the container here or in Portainer, you will still it in Portainer

Done!
