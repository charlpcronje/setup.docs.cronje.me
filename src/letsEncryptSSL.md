# Let's Encrypt Free Wildcard SSL Certificate

## Via NginX Proxy Manager

Here is the problem I'm facing... I want to have multi-level sub-domains for examele

*.docs.CRONje.ME

I would have thought a wildcard certificate for CRONje.ME would be sufficient, but it is not. A wildcard certificate for CRONje.ME only covers `*.CRONje.ME` and not for `*.docs.CRONje.ME`

So to get past this problem I need more wildcard certificates and I don't want to pay for them. So this is how:

- The easiest way is to install [NginX Proxy Manager](https://setup.docs.CRONje.ME/nginxproxymanager)
- From there you can click on Add Proxy Host
- On The SSL tab, Select request SSL Certificat
- Either complete DNS Challenge or enter email address. But you can't request a wildcard certificat without DNS Chanllenge and my host `ionos.com` don't give out API keys for free

## Via Acme PHP

Acme PHP is available as a single PHAR file to download on Github. For security purposes, this PHAR file is signed using OpenSSL to ensure you are using a valid Acme PHP binary.

[Acme PHP Setup](acmephp.md)
