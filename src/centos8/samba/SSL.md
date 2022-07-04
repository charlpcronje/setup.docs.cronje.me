---
title: Disable Certificate Check
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

```shell
composer config --global --list ?

composer config --global disable-tls true
composer config --global secure-http false
composer config --global repo.packagist composer http://packagist.org
```