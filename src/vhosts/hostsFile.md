---
title: Set Up Local Hosts File
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

If your DNS is not point on the same server then you can simply check the functionality of the website by enter the IP and Domain in the `/etc/hosts` file.

> Note - You have to enter these details in the host OS (Windows Hosts File)

```shell
code C:\WINDOWS\System32\drivers\etc\hosts
```

```hosts
Server-Ip-Address    securezone.co.za
Server-Ip-Address    graph.securezone.co.za
Server-Ip-Address    api.securezone.co.za
Server-Ip-Address    old.securezone.co.za
```
