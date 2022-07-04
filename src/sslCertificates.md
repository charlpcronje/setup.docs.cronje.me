---
title: Install SSL Certificates
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

SSL Certificates are small data files that certify ownership of a public cryptographic key. Certificate Authorities (CA) guarantee that the key belongs to an organization, server, or other entity listed in the certificate.

When a user, via their browser, accesses a certified website, the information is encrypted with a unique public key. The data can only be decrypted by using a unique private key located on the host server. This high level of encryption prevents unauthorized attempts to access the information.

## Prerequisites

- A user with `sudo` privileges
- Access to a command line (`Ctrl-Alt-T`)
- A `CentOS 7` machine
- A valid domain name with `DNS pointed` at the server

## How to Get an SSL Certificate

There are several ways to obtain Certificates:

1. Using an automated and free certificate authority such as the Let’s Encrypt project.
2. Commercial certificate authorities provide certificates for a fee (Comodo, DigiCert, GoDaddy)
3. Alternatively, it is possible to create a self-signed certificate. This type of certificate is useful for testing purposes or for use in a development environment.

If you are still considering what type of certificate you need, or which CA to choose, we’ve prepared a comprehensive guide to SSL certificates, private keys, and CSRs to assist you in the process.

> **Note:** Trusted CAs do not verify self-signed certificates. Users cannot use it to validate the identity of their server automatically.

## Install SSL Certificate with Let’s Encrypt

Let’s Encrypt is a free, open, and automated certificate authority. It uses the certbot software tool to administer certificates automatically.

Certbot is a highly automated tool. Make sure that that your Apache installation is valid and that you have a virtual host configured for your domain/s. You should first read our tutorial on how to install Apache on CentOS 7 if you need assistance with configuring your firewall and virtual hosts.

## Certbot Installation

1. Use the command terminal to install the EPEL repository and yum-utils:

```shell
sudo yum –y install epel-release yum-utils
```

1. Next, install a module that supports SSL for Apache:

```shell
sudo yum -y install mod_ssl
```

In this example, the latest version of the module is already available.

![term](https://phoenixnap.com/kb/wp-content/uploads/2021/04/install-ssl-mod-apache.png)

1. We can now install certbot for Apache:

sudo yum –y install python-certbot-apache

1. Once the installation runs its course, you can start the process to obtain a certificate by entering:

```shell
sudo certbot –apache –d yourdomain.com
```

Alternatively, start certbot by typing:

```shell
sudo certbot
```

1. The client asks you to provide an email address and to read and accept the Terms of Services. Certbot then lists the domains available on your server. Activate HTTPS for specific domains or all of them by leaving the field blank.

![term2](https://phoenixnap.com/kb/wp-content/uploads/2021/04/certbot-client-lets-encrypt.png)

The next prompt allows you to force all requests to secure HTTPS access.

Once you have made your choices, the message on the terminal confirms that you have enabled encryption for your domain.

## Automatic Certificate Renewal

The certificates issued by Let’s Encrypt are valid for 90 days. The certbot renew command checks the installed certificates and tries to renew them if they are less than 30 days away from expiration. To automate this process, create a cron job to execute the command periodically.

Use your preferred text editor to define how often to execute the renew command:

```shell
sudo crontab -e
```

Enter this line and save the crontab:

```cron
* */12 * * * /usr/bin/certbot renew >/dev/null 2>&1
````

## How to Install SSL Certificate with Comodo

1. The first step is to submit a Certificate Signing Request to a Certification Authority. Our detailed guide on how to generate a certificate signing request (CSR) with OpenSSL is an excellent resource if you need assistance with this process.

1. Once a CA certifies your request, you receive a copy of your SSL certificate. You can now install the certificate on your CentOS 7 server.

This example shows how to install a certificate from a paid SSL provider, Comodo.

1. Once Comodo verifies your CSR the request, download the SSL files. Copy them (ComodoRSACA.crt) and the Primary Certificate (yourdomain.crt), to your Apache server directory. The private key generated during the CSR (Certificate Signing Request) process needs to be on the same server.

## Configure Virtual Hosts for SSL

After you have successfully certified the domain and placed the key files on the server, the next step will be to configure the virtual hosts to display the certificate.

1. Access the SSL configuration file:

```shell
sudo nano /etc/httpd/conf.d/ssl.conf
```

1. Edit the configuration file to point to the correct files on your server.

Uncomment the following lines under section <VirtualHost_default_:443> and enter the correct file paths:

- DocumentRoot “/var/www/yourdomain.com”
- ServerName yourdomain.com: 443

![ter3](https://phoenixnap.com/kb/wp-content/uploads/2021/04/edit-config-virtual-host-comodo-ssl.png)

- General Host for Virtual Host
- SSLEngine on
- SSLCertificateFile – The path of your certificate file.
- SSLCertificateKeyFile – The path of your key file.
- SSLCertificateChainFile– The intermediate COMODO certificate file.

![Ter5](https://phoenixnap.com/kb/wp-content/uploads/2021/04/config-comodo-ssl-apache.png)

1. After making the necessary changes, exit the file (Ctrl+X), and press y to save the changes.

1. Test your Apache configuration before restarting. Make sure that the syntax is correct by typing:

```shell
sudo apachectl configtest
```

Once the system confirms that the syntax is correct, restart Apache:

```shell
sudo systemctl restart httpd
```

You have now set up your Apache server to use the SSL certificate.

## How to Create a Self-signed SSL Certificate

A self-signed certificate is useful for testing, in development environments, and on an intranet.

1. As with Let’s Encrypt, the mod_ssl Apache module provides support for the SSL encryption:

```shell
sudo yum –y install mod_ssl
```

1. Create a new directory to store the private key:

```shell
sudo mkdir /etc/ssl/privatekey
```

1. Restrict access to that directory only to the root user:

```shell
sudo chmod 700 /etc/ssl/privatekey
```

1. Generate a self-signed certificate using this OpenSSL command:

```shell
sudo openssl req -x509 -new -newkey rsa:2048  -nodes -days 365 -keyout /etc/ssl/privatekey/ yourdomain.key -out /etc/ssl/certs/yourdomain.csr
```

This is a detailed overview of the elements:

- `openssl` – activates the OpenSSL software
- `req` – indicates that we require a CSR
- `-x509` – specifies to use the X.509 signing request
- `-new -newkey` – generate a new key
- `rsa:2048` – generate a 2048-bit RSA mathematical key
- `-nodes` – no DES, meaning do not encrypt the private key in a PKCS#12 file
- `–days 365`– number of days that the certificate is valid for
- `-keyout` – indicates the domain you’re generating a key for
- `-out` – specifies the name of the file that contains the CSR
- Note: Make sure to replace yourdomain with your actual domain.

1. The system launches a questionnaire for you to fill out.

Enter your information in the available fields:

- **Country Name** – use a 2-letter country code
- **State** – the state where the domain owner is incorporated in
- **Locality** – the city where the domain owner is incorporated in
- **Organization** name – an entity that owns the domain
- **Organizational unit name** –the department or group in your organization that works with certificates
- **Common name** – most often, the fully qualified domain name (FQDN)
- **Email address** – contact email address
- **Challenge password** – define an optional password for your key pair

The image represents an example questionnaire in CentOS 7.

![questionnaire](https://phoenixnap.com/kb/wp-content/uploads/2021/04/self-signed-certificate-csr-cento-7.png)

## Example questionnaire in CentOS 7

1. Proceed to configure the virtual host to display the new certificate. The process is identical to the steps outlined in Chapter 2, Configure Virtual Hosts for SSL.

1. Test your Apache configuration before restarting. To make sure that the syntax is correct, type:

```shell
sudo apachectl configtest
```

1. Once the system confirms that the syntax is correct, restart Apache:

```shell
sudo systemctl restart httpd
```

You have now set up your Apache server to use your self-signed `SSL` certificate and should be able to visit your site with `SSL` enabled.

### How to Check if a `SSL` Certificate is Valid?

To check if a `SSL` Certificate is valid  you can publicly available services, such as the SSL Server Test. Confirm the status of your certificate, and to check if all the details are correct.

Alternatively, access your website using `https://` to see if the `SSL` certificate is visible. The green padlock indicates that the additional layer of encryption is present
