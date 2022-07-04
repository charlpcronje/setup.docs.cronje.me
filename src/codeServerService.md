---
title: VS Code Server as a Service
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

You’ll store the service configuration in a file named `code-server.service`, in the `/usr/lib/systemd/system` directory, where systemd stores its services.

## Step 1: Create the service, start and enable

```shell
sudo nano /usr/lib/systemd/system/code-server.service
```

The file will be empty, add the following lines

```shell
[Unit]
Description=code-server

# If you are not Running nginx but apache or whatever else, then comment out the line below
# This line below instructs VS code to start after nginx 

# After=nginx.service

[Service]
Type=simple
# Change the password
Environment=PASSWORD=your_password
# Change IP Address and port     
ExecStart=/usr/bin/code-server --bind-addr 127.0.0.1:8080 --user-data-dir /var/lib/code-server --auth password
Restart=always

[Install]
WantedBy=multi-user.target
```

Here you first specify the description of the service. Then, you state that the nginx service must be started before this one. After the [Unit] section, you define the type of the service (simple means that the process should be simply run) and provide the command that will be executed.

You also specify that the global code-server executable should be started with a few arguments specific to code-server. --bind-addr 127.0.0.1:8080 binds it to localhost at port 8080, so it’s only directly accessible from inside of your server. --user-data-dir /var/lib/code-server sets its user data directory, and --auth password specifies that it should authenticate visitors with a password, specified in the PASSWORD environment variable declared on the line above it.

Remember to replace your_password with your desired password, then save and close the file.

The next line tells systemd to restart code-server in all malfunction events (for example, when it crashes or the process is killed). The [Install] section orders systemd to start this service when it becomes possible to log in to your server.

Start the code-server service by running the following command:

```shell
sudo systemctl start code-server
```

Check that it’s started correctly by observing its status:

```shell
sudo systemctl status code-server
```

You’ll see output similar to:

```shell
Output
● code-server.service - code-server
   Loaded: loaded (/usr/lib/systemd/system/code-server.service; disabled; vendor preset: disabled)
   Active: active (running) since Wed 2020-05-13 19:57:27 UTC; 5s ago
 Main PID: 10608 (node)
   CGroup: /system.slice/code-server.service
           ├─10608 /usr/lib/code-server/node /usr/lib/code-server/out/node/entry.js --bind-addr 127.0.0.1:8080 --user-data-dir /var/lib/code-server --auth...
           └─10622 /usr/lib/code-server/node /usr/lib/code-server/out/node/entry.js --bind-addr 127.0.0.1:8080 --user-data-dir /var/lib/code-server --auth...

May 13 19:57:27 code-server-update-centos systemd[1]: Started code-server.
May 13 19:57:27 code-server-update-centos code-server[10608]: info  code-server 3.2.0 fd36a99a4c78669970ebc4eb05768293b657716f
May 13 19:57:27 code-server-update-centos code-server[10608]: info  HTTP server listening on http://127.0.0.1:8080
May 13 19:57:27 code-server-update-centos code-server[10608]: info    - Using custom password for authentication
May 13 19:57:27 code-server-update-centos code-server[10608]: info    - Not serving HTTPS
May 13 19:57:27 code-server-update-centos code-server[10608]: info  Automatic updates are enabled
```

To make code-server start automatically after a server reboot, enable its service by running the following command:

```shell
sudo systemctl enable code-server
```

In this step, you’ve downloaded code-server and made it available globally. Then, you’ve created a systemd service for it and enabled it, so code-server will start at every server boot. Next, you’ll expose it at your domain by configuring Nginx to serve as a reverse proxy between the visitor and code-server.

## Step 2 — Exposing code-server at Your Domain

In this section, you will configure Nginx as a reverse proxy for code-server.

As you have learned in the Nginx prerequisite step, its site configuration files are stored under /etc/nginx/conf.d and will automatically be loaded when Nginx starts.

You’ll store the configuration for exposing code-server at your domain in a file named code-server.conf, under /etc/nginx/conf.d. Start off by creating it using your editor:

```shell
sudo vi /etc/nginx/conf.d/code-server.conf
```

```shell
server {
    listen 80;
    listen [::]:80;

    server_name code-server.your-domain;

    location / {
        proxy_pass http://localhost:8080/;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection upgrade;
        proxy_set_header Accept-Encoding gzip;
    }
}
```

Replace `code-server.your-domain` with your desired domain, then save and close the file.

In this file, you define that Nginx should listen to HTTP port `80`. Then, you specify a `server_name` that tells Nginx for which domain to accept requests and apply this particular configuration.

In the next block, for the root location (/), you specify that requests should be passed back and forth to code-server running at `localhost:8080`. The next three lines (starting with `proxy_set_header`) order Nginx to carry over some HTTP request headers that are needed for correct functioning of WebSockets, which code-server extensively uses.

To test the validity of the configuration, run the following command:

```shell
sudo nginx -t
```

You’ll see the following output:

```shell
Output
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

For the configuration to take effect, you’ll need to restart Nginx:

```shell
sudo systemctl restart nginx
```

`CentOS 7` comes with SELinux turned on, with a strict `ruleset`, which by default does not permit Nginx to connect to local TCP sockets. Nginx needs to do in order to serve as a reverse proxy for `code-server`. Run the following command to relax the rule permanently:

```shell
sudo setsebool httpd_can_network_connect 1 -P
```

Then, in your browser, navigate to the domain you used for `code-server`. You will see the `code-server` login prompt.

`code-server` is asking you for your password. Enter the one you set in the previous step and press **Enter IDE**. You’ll now enter code-server and immediately see its editor GUI

You now have your code-server installation accessible at your domain. In the next step, you’ll secure it by applying a free Let’s Encrypt TLS certificate.

## Step 3 — Securing Your Domain

In this section, you will secure your domain using a Let’s Encrypt TLS certificate, which you’ll provision using `Certbot`.

To install the latest version of `Certbot` and its Nginx plugin, run the following command:

```shell
sudo yum install certbot python2-certbot-nginx -y
```

To request certificates for your domain, run the following command:

```shell
sudo certbot --nginx -d code-server.your-domain
```

In this command, you run certbot to request certificates for your `domain—you` pass the domain name with the -d parameter. The `--nginx` flag tells it to automatically change Nginx site configuration to support `HTTPS`. Remember to replace code-server.your-domain with your domain name.

If this is your first time running Certbot, you’ll be asked to provide an email address for urgent notices and to accept the EFF’s Terms of Service. Certbot will then request certificates for your domain from Let’s Encrypt. It will then ask you if you’d like to redirect all `HTTP` traffic to `HTTPS`:

```shell
# Output
Please choose whether or not to redirect `HTTP` traffic to `HTTPS`, removing `HTTP` access.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel):
```

It is recommended to select the second option in order to maximize security. After you input your selection, press `ENTER`.

The output will be similar to this:

```shell
# Output
IMPORTANT NOTES:
- Congratulations! Your certificate and chain have been saved at:
 /etc/letsencrypt/live/code-server.your-domain/fullchain.pem
 Your key file has been saved at:
 /etc/letsencrypt/live/code-server.your-domain/privkey.pem
 Your cert will expire on ... To obtain a new or tweaked
 version of this certificate in the future, simply run `certbot` again
 with the "certonly" option. To non-interactively renew *all* of
 your certificates, run "certbot renew"
- Your account credentials have been saved in your `Certbot`
 configuration directory at /etc/letsencrypt. You should make a
 secure backup of this folder now. This configuration directory will
 also contain certificates and private keys obtained by `Certbot` so
 making regular backups of this folder is ideal.
- If you like `Certbot`, please consider supporting our work by:

 Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
 Donating to EFF:                    https://eff.org/donate-le
```

This means that Certbot has successfully generated TLS certificates and applied them to the Nginx configuration for your domain. You can now reload your code-server domain in your browser and observe a padlock to the left of the site address, which means that your connection is properly secured.

Now you’ll make Certbot automatically renew the certificates before they expire. To run the renewal check daily, you’ll use cron, a standard system service for running periodic jobs. You direct cron by opening and editing a file called a crontab:

```shell
sudo crontab -e
```

This command will open the default crontab, which is currently an empty text file. Add the following line, then save and close it:

```shell
15 3 * * * /usr/bin/certbot renew --quiet
```

`15 3 * * *` will run the following command at `3:15` am every `day—you` can adapt this to any time.

The renew command for Certbot will check all certificates installed on the system and update any that are set to expire in less than thirty days. `--quiet` tells Certbot not to output information or wait for user input.

`cron` will now run this command daily. All installed certificates will be automatically renewed and reloaded when they have thirty days or less before they expire.

Now that you have code-server accessible at your domain through a secured Nginx reverse proxy, you’re ready to review the user interface of code-server.
