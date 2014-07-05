---
layout: post
title: GNU Privacy Guard (GPG) examples using Golang
date: 2014-07-04 14:35
---

Someone wrote to me today that they found some of my public Github Gists "public_key_decrypt|encrypt_gpg_base64.go and encrypt_decrypt_gpg_armor.go - incredibly helpful! Thanks for sharing those. I'm using the latter for storing bitcoin private keys."

I originally wrote them as there weren't any good examples on the web that ran through different scenarios.

As part of the process I wrote a program called [Jaeger](https://github.com/jyap808/jaeger) which is a JSON encoded GPG encrypted key value store. It is useful for generating and keeping configuration files secure.

Here is a compilation of my code examples.

* [Decrypting an ASCII armored GPG encrypted string in Golang](https://gist.github.com/jyap808/8250067)
* [Symmetrically encrypting a string into ASCII armored GPG format and then Decrypting it in Golang](https://gist.github.com/jyap808/8250124)
* [Decrypting an ASCII armored GPG encrypted string using a passphrase protected private key in ASCII armor format](https://gist.github.com/jyap808/8309947)
* [Decrypting an ASCII armored GPG encrypted string using a private key (no passphrase) in ASCII armor format](https://gist.github.com/jyap808/8310117)
* [Public key encrypting a string into GPG format and outputting it in base64 encoding](https://gist.github.com/jyap808/8324818)
* [Decrypting a base64 GPG public key encrypted string using a passphrase protected private key in ASCII armor format](https://gist.github.com/jyap808/8341483)

