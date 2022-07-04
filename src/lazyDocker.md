---
title: Installing LazyDocker
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

## What is LazyDocker

Memorising docker commands is hard. Memorising aliases is slightly less hard. Keeping track of your containers across multiple terminal windows is near impossible. What if you had all the information you needed in one terminal window with every common command living one keypress away (and the ability to add custom commands as well). Lazydocker's goal is to make that dream a reality

For more info on LazyDocker visit the [GitHub Repo](https://github.com/jesseduffield/lazydocke)

## Install LazyDocker

I found installing Lazy Docker via GO was the quickest way and I'm hesitant to let something that is reporting on Docker be run on top of Docker for obvious reasons to.

If you haven't installed GoLang yet then got to [Installing Golang](goLang.md) first and come back.

After you installed GoLang then run the following command to install LazyDocker

```shell
go install github.com/jesseduffield/lazydocker@latest
```

Then to run LazyDocker run the following command:

```shell
lazydocker
```

Done!
