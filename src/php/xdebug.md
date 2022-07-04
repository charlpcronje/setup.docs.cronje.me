---
title: X-Debug Install
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

[https://linuxconfig.org/how-to-install-xdebug-on-redhat-8](https://linuxconfig.org/how-to-install-xdebug-on-redhat-8)
```

## Install dependencies

```shell
sudo dnf install php php-devel php-pear
sudo pecl install xdebug
sudo nano /etc/php.d/30-xdebug.ini
```

pecl install xdebug
