# Public key cryptography: GPG, OpenPGP, PGP

## Rationale

I wanted to set up commit signature verification for GitHub to get a nice green **Verified** badge next to my commits. GitHub even has a guide for this: [Managing commit signature verification][github]. How difficult could that be?

Christ on a bike, that was quite an adventure.

Basically, I wanted to generate a PGP key _without a passphrase_ (or clear the passphrase after the keys had been generated) and make Git client pick up that key and use it to sign my commits. My whole disk is encrypted, and I am not going to be using this PGP key for anything else (it's easily revokeable on GitHub), so I believe this is a good compromise between security and usability.

[github]: https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification

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

## Where we are now...

When people say "PGP keys" or "PGP certificates" they _most often_ mean OpenPGP-compliant keys. These keys are _often_ produced by the free and open GPG program. But there are other implementations. The point is that although the term "PGP key" has remained, the original PGP _program_ is pretty much history. And OpenPGP is a standard, not a program.

Lots and lots of "advice" on GPG on the Internet is of grotesquely bad quality. It either refers to the obsolete versions of software, or shows almost complete lack of understanding of how GPGv2 operates. The manual for GPGv2 is not much help, as it's very concise, reference-style, and IMO not very user friendly. So I had a hard time figuring it out. Scavenging through all available sources of information, I developed an understanding of the mental model behind GPGv2 set of tools, and the actual solution turned out to be very simple.

## Install GPG on Linux

It doesn't get any better when it comes to Ubuntu package names!

As of Ubuntu 20.04 LTS:

> Install `gnupg` and ignore the rest!

The mess is due to:

* an old, obsolete version of GPG (version `1`) still being distributed, for some reason, alongside a more modern version `2`.
* the modern version `2` is offered in two flavours: a bare minimum (`gpg`), and the full suite (`gnupg`)

For the adventurous, this is the actual situation with the packages:

* There is a `gpg` package which installs the main GPG application. This is useful in itself, but check for `gnupg` below.
* There is also a `gnupg` package, which is a superset of the above package. It provides the full suite of GPG applications.
* There is also a `gnupg1` package which is for an obsolte version of the suite, so don't use it.
* There is also a `gnupg2` package, which a _dummy transitional name_ for `gnupg`, so don't use it.
* There is _no_ `gpg2` package.
