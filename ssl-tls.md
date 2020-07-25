# Stop using SSL

The term **SSL** *must* go out of fashion and the time is *now*. It refers to an obsolete and insecure protocol.

## What is SSL?

SSL, or Secure Sockets Layer, **was** an encryption-based Internet security protocol. It was first developed by Netscape in 1995 for the purpose of ensuring privacy, authentication, and data integrity in Internet communications. 

SSL has not been updated since SSL 3.0 in 1996 and is now considered to be **deprecated**. There are several known vulnerabilities in the SSL protocol and security experts recommend discontinuing its use. In fact, most modern web browsers **no longer support SSL at all**.

## The future is TLS

Transport Layer Security, or TLS, is a direct successor of long obsolete SSL security protocol.

TLS was proposed by the Internet Engineering Task Force (IETF), an international standards organization, and the first version of the protocol was published in 1999. The **most recent version is TLS 1.3**, which was published in 2018.

## Certificates are not the same as protocols

The *certificates* are not dependent on *protocols*. While many vendors tend to use the phrase *SSL/TLS Certificate*, it may be more accurate to call them *Certificates for use with SSL and TLS*, since the protocols are determined by the server configuration, not the certificates themselves.

That goes for encryption strength, too. Many certificates advertise encryption strength, but it’s the capabilities of the server and the client that determine that. At the beginning of each connection, a process called a *handshake* occurs. During this process, the client authenticates the server’s TLS certificate and the two decide on a mutually supported *cipher suite*.

Cipher suites are a collection of algorithms that all work together to securely encrypt the connection with a website. When the cipher suite is negotiated during the handshake, that’s when the version of the protocol and the supporting algorithms are determined. The certificate just facilitates the process.

Historically, there have been four algorithms in a cipher suite:

* Key exchange
* Digital signature
* Message authentication
* Hashing algorithm

## The handshake process

TLS 1.3 handshake is accomplished with a single roundtrip and enables *Zero roundtrip resumption* (0-RTT). Part of the way this was done was by reducing the number of cipher suites it supports, from four algorithms to two:

* Bulk encryption (symmetric/session) algorithm
* Hashing algorithm

The *key exchange* and *digital signature* negotiations have been removed.

*Key exchange* is now performed using a Diffie-Hellman family, which both enables perfect forward secrecy by default and allows the client and server to provide their portion of the shared secret on their first interaction. That first interaction is now encrypted, too, shutting the door on a possible attack vector.

## Server configuration

Disable SSL 2.0 and 3.0 and TLS 1.0 and 1.1.

## What’s the difference between TLS and HTTPS?

HTTPS is an implementation of TLS encryption on top of the HTTP protocol, which is used by all websites as well as some other web services. Any website that uses HTTPS is therefore employing TLS encryption.

## Further Reading

The point of this note is to highlight the *annoying persistence* with which the old protocol name is still being used almost interchangeably with the new protocol name. This is just wrong.

* [Using Transport Layer Security (TLS) in your organisation](https://www.gov.uk/government/publications/email-security-standards/transport-layer-security-tls) (gov.uk)
* [TLS 1.3: better for individuals - harder for enterprises](https://www.ncsc.gov.uk/blog-post/tls-13-better-individuals-harder-enterprises) (gov.uk NCSC)
* [Introducing TLS 1.3](https://blog.cloudflare.com/introducing-tls-1-3/) (Cloudflare)
* [An Overview of TLS 1.3 – Faster and More Secure](https://kinsta.com/blog/tls-1-3/) (Kinsta)

&mdash; Oliver Frolovs, 2020