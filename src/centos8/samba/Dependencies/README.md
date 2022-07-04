---
title: COMPOSER DEPENDENCIES
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

## 1. Before adding any requirements into you composer.json

```shell
# Browse to the document root of the website
echo "{}" >> composer.json
composer update
```

This will already create a vendor folder an `autoloader.php`. This will be the only file you will ever include for any vendor dependencies ever. No matter what dependencies you install, you will always just keep on including that one `autoloader.php`

## 2. Add dependency to composer.json

```shell
nano composer.json
{
    "require": {
        "phpmailer/phpmailer": "6.5.1"
    }
}
```

## 3. Let Composer update all the dependencies

```shell
composer update
```

Now you dependencies you required will be installed and they will be autoloaded if you just include the `/vendor/autoloader.php`
