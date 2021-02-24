# Public key cryptography: GPG, OpenPGP, PGP

Christ on a bike, this is messy!

## History

### PGP

> PGP was a proprietary program (and a standard) facilitating encrypted communication resistant to eavesdropping attacks.

PGP, also known as [Pretty Good Privacy][pgp], was originally created by Phil Zimmerman in 1991. It provides cryptographic privacy and authentication for data communication. It's proprietary, and for some reason it still exists, but don't use it. It's both a software and an underlying standard.

### OpenPGP

> OpenPGP is an _encryption standard_ supported by the IETF. It's modern, but it's only a standard, not a program.

Due to the patent issues, PGP was not always practical for international use. In 1997, Phil Zimmerman made a proposal to the [IETF][ietf] for the creation of an open-source PGP standard. The proposal was accepted and led to the creation of the OpenPGP _protocol_, which defines standard formats for encryption keys and messages. So, OpenPGP is a _IETF standard_ [RFC4880][rfc4880], there is no _program_ named OpenPGP.

Naturally, many implementations of this standard exist.

### GPG

> GPG is a suite of programs for encrypting data and communications in a way compatible with the OpenPGP standard.

GPG, also known as [GNU Privacy Guard][gpg] is a complete and free implementation of the OpenPGP _standard_. It is a suite of programs allowing you to encrypt and sign your data and communications.

[pgp]: https://en.wikipedia.org/wiki/Pretty_Good_Privacy
[ietf]: https://en.wikipedia.org/wiki/Internet_Engineering_Task_Force
[rfc4880]: https://tools.ietf.org/html/rfc4880
[gpg]: https://en.wikipedia.org/wiki/GNU_Privacy_Guard

## Useful terminology

When people say "PGP keys" or "PGP certificates" they _most often_ mean OpenPGP-compliant keys. These keys are _often_ produced by the free and open GPG program. But there are other implementations. The point is that although the term "PGP key" has remained, the original PGP _program_ is pretty much history. And OpenPGP is a standard, not a program.
