# Enable HTTPS with Let's Encrypt CA

:warning: A reminder that **SSL** standard had not been updated since 1996. [Stop Using SSL](ssl-tls.md)!
:heart: The current standard is **TLS**. This is the term to use.

## dev domains

[get.dev](https://get.dev/) explains Google's new gTLD: the `.dev` top-level domain is included on the HSTS preload list, making HTTPS required on all connections to `.dev` websites and pages withouth needing individual HSTS registration or configuration. Security is built in.

## Certificate Authorities (CA)

[Let's Encrypt](https://letsencrypt.org/) is a **modern** *Certificate Authority* using *ACME* protocol.

## Web server configuration

Use [Mozilla SSL Configuration Generator](https://ssl-config.mozilla.org/) to generate the web server application configuration.

Options (set both):

* **HSTS** (HTTP Strict Transport Security) &mdash; [WikiPedia Article](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security)
* **OCSP Stapling**, or the *Online Certificate Status Protocol stapling*, formally known as the *TLS Certificate Status Request extension* &mdash; is a standard for checking the **revokation** of certificates.

More guidance: 

The article [Let's Encrypt my servers with acme tiny][1] explains the use of `acme-tiny` and *Ansible*.

[1]: (https://xdeb.org/post/2016/02/09/lets-encrypt-my-servers-with-acme-tiny/)

## Testing web server configuration

Use [SSL Labs](https://www.ssllabs.com/ssltest/index.html).

## Renewal of certificates

* Issued certificates expire in three monts, so must auto-renew.  [Using systemd as a better cron](https://www.ssllabs.com/ssltest/index.html)
* EFF issued the *certbot* software, which can renew the certificates: [Certbot](https://certbot.eff.org/). [Certbot documentation](https://certbot.eff.org/docs/) is extensive.

:warning: Certbot must be installed *on the server*, but it needs a whole lot of Python libraries. What's the best practice?