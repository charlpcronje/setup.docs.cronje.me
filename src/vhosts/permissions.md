---
title:
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script># Grant Permissions

All the files and directories are owned by the `root` user. If you want to allow the other user to access and modify the files in the Document Root then you can change the ownership with the `chown` command.

```shell
chown -R apache:apache /var/www/securezone.co.za/public_html
chown -R apache:apache /var/www/api.securezone.co.za/public_html
```

Now we have to change the permission to ensure that read permission allowed to the general web directory. So, that all the content inside the public_html can be served correctly.

```shell
sudo chmod -R 755 /var/www
```
