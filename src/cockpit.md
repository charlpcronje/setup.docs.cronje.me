# Install Cockpit on CentOS 7

## Installation

```shell
sudo yum install cockpit
```

## Enable cockpit

```shell
sudo systemctl enable --now cockpit.socket
```

## Open the firewall if necessary

```shell
sudo firewall-cmd --permanent --zone=public --add-service=cockpit
sudo firewall-cmd --reload
```

## Make Cockpit proxy aware

To make cockpit proxy aware so that you can run it via NginX Reverse Proxy you need to do the following

For security Cockpit will be unable to serve requests from origins it is unfamiliar with due to cross domain limitations. In our example, Cockpit will see the origin as cockpit.domain.tld however it will believe it's running on `127.0.0.1` and therefore be unable to serve the request.

To make Cockpit proxy aware, you will need to modify the Cockpit config file located at `/etc/cockpit/cockpit.conf`. This file may not exist and if it doesn't you should create it.

```conf
[WebService]
Origins = https://cockpit.CRONje.ME wss://cockpit.CRONje.ME
ProtocolHeader = X-Forwarded-Proto
```

These changes will let Cockpit know that connections will come through for https (secure http) and wss (secure websockets) on the subdomain cockpit.domain.tld, and that it should look for the X-Forwarded-Proto header to determine if the connection is secure or not, this is important as Cockpit will redirect any non-local connection from http to https automatically and sees cockpit.domain.tld is non-local.

Once these changes are made you will need to restart cockpit.

## Error ERR_TOO_MANY_REDIRECTS

proxy_pass `http://127.0.0.1:9090`; to proxy_pass `https://127.0.0.1:9090`;

So in your NginX Proxy Manger, set the `Scheme` to `https`
