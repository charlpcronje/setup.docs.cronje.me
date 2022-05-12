# Apache Config

I went to devserve.me in my browser but nothing was showing, I check and apache was listening on port 80.

But the following settings needed to be changed.

- The IP Address it was listening on needed to be changed from 127.0.0.1 to the server's IP address
- The hostname it was listening on needed o be changed from www.example.com to the server's hostname

After I updated that and restarted the service, it work fine.

config file location `/etc/httpd/conf/httpd.conf`

Restart service

```shell
systemctl restart httpd
```
