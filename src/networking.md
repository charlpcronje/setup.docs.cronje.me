---
title: Network Config
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

The easiest way is to use the GUI Aki7lol

```shell
system-config-network

service network restart
```

For communication between VirtualBox and Windows, set the network device to bridged mode in VirtualBox Settings.
This will cause the virtual machine to be seen as just another device on the network and the DHCP will assign it an IP Address

If you are working with a cloned device you will need to set the Device Mac address to the address of the device as it is specified in VirtualBox
