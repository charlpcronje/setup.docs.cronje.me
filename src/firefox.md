---
title: Installing Firefox
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

In the past I struggled to get this to work, I'm going to try again.

Try installing 

```sh
yum install  xorg-x11-server-Xorg xorg-x11-xauth xorg-x11-apps -y
```

If the repo is down try installing this way

```sh
wget http://mirror.centos.org/centos/7/updates/x86_64/Packages/xorg-x11-server-Xorg-1.20.4-16.el7_9.x86_64.rpm
```

```shell
mkdir /srv/tools
wget -O- "https://download.mozilla.org/?product=firefox-latest-ssl&os=linux64&lang=en-US" | tar -jx -C /srv/tools/
```

Create a symlink to a newly downloaded `/srv/tools/firefox/firefox` executable.

```shell
ln -s /srv/tools/firefox/firefox /usr/bin/firefox
```

Start the latest Firefox browser from GUI menu or by executing the `firefox` command.

```shell
firefox
```

If you get an error like this:

```shell
libgtk-3.so.0: cannot open shared object file: No such file or directory
```

Then you need to install GTK3

```shell
yum install gtk3-devel

# Run Firefox again
firefox
```

Getting this error?

```shell
Error: no DISPLAY environment variable specified
```

That means everything is working, now you just need to specify your local display for displaying the browser, for that you need to have X11 forwarding and an XServer. But no big deal, just two quick steps here

[X11 Forwarding](https://tip.docs.cronje.me/x11forwarding)
