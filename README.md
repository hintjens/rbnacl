![RbNaCl](https://raw.github.com/cryptosphere/rbnacl/master/images/logo.png)
======
[![Build Status](https://travis-ci.org/cryptosphere/rbnacl.png?branch=master)](https://travis-ci.org/cryptosphere/rbnacl)
[![Code Climate](https://codeclimate.com/github/cryptosphere/rbnacl.png)](https://codeclimate.com/github/cryptosphere/rbnacl)

A Ruby binding to the state-of-the-art [Networking and Cryptography][nacl]
library by Daniel J. Bernstein. This is **NOT** Google Native Client. This
is a crypto library.

On a completely unrelated topic, RbNaCl is also the empirical formula for
Rubidium Sodium Chloride.

Need help with RbNaCl? Join the [RbNaCl Google Group][group]

[nacl]: http://nacl.cr.yp.to/
[group]: http://groups.google.com/group/rbnacl

## Why NaCl?

NaCl is a different kind of cryptographic library. In the past crypto
libraries were kitchen sinks of little bits and pieces, like ciphers,
MACs, signature algorithms, and hash functions. To accomplish anything
you had to make a lot of decisions about which specific pieces to use,
and if any of your decisions were wrong, the result was an insecure
system. The choices are also not easy: EAX? GCM? CCM? AES-CTR? CMAC?
OMAC1? AEAD? NIST? CBC? CFB? CTR? ECB? OMGWTFBBQ!

NaCl puts cryptography on Rails! Instead of making you choose which
cryptographic primitives to use, NaCl provides convention over configuration
in the form of expertly-assembled high-level cryptographic APIs that ensure
not only the confidentiality of your data, but also detect tampering.
These high-level, easy-to-use APIs are designed to be hard to attack by
default in ways primitives exposed by libraries like OpenSSL are not.

This approach makes NaCl a lot closer to a system like GPG than it is
to the cryptographic primitive APIs in a library like OpenSSL. In addition,
NaCl also uses state-of-the-art encryption, including Curve25519 elliptic
curves and the XSalsa20 stream cipher. This means with NaCl you not only get
a system which is designed to be secure-by-default, you also get one which
is extremely fast with comparatively small cryptographic keys.

For more information on NaCl's goals, see Dan Bernstein's presentation
[Blaming the Cryptographic User](http://cr.yp.to/talks/2012.08.08/slides.pdf)

## Supported platforms

You can use RbNaCl anywhere you can get libsodium installed (see below).
RbNaCl is continuously integration tested on the following Ruby VMs:

* MRI 1.8 / REE
* MRI 1.9 (YARV)
* JRuby 1.7 (in both 1.8/1.9 mode)
* Rubinius HEAD (in both 1.8/1.9 mode)

In theory Windows should be supported, although there are not yet any
reports of successful Windows users.

## Installation

### libsodium

RbNaCl is implemented as a Ruby FFI binding, which is designed to bind to
shared libraries. Unfortunately NaCl does not presently ship a shared library,
so RbNaCl cannot take advantage of it via FFI. RbNaCl will support usage with
the upstream NaCl once it is able to compile a shared library.

For now, to use RbNaCl, you will need to install libsodium, a portable version
of NaCl based upon the reference C code. Please see the libsodium project
for information regarding installation:

https://github.com/jedisct1/libsodium

#### OS X

Unfortunately libsodium is not in homebrew proper yet (I would strongly
encourage you to [ask for libsodium's inclusion in homebrew][homebrew]),
however you can use homebrew's "tap" feature for the time being to
install libsodium:

```
brew tap qmx/homebrew-libsodium
brew install libsodium
```

[homebrew]: https://github.com/mxcl/homebrew/pull/17275

### RbNaCl gem

Once you have libsodium installed, add this line to your application's Gemfile:

    gem 'rbnacl'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rbnacl

## Documentation

RbNaCl's documentation can be found [in the Wiki][wiki]. The following features
are supported:

* [Secret-key Encryption][secretkey]: authenticated symmetric encryption using a
  single key shared among parties
* [Public-key Encryption][publickey]: securely send messages to a given public
  key which can only be decrypted by a secret key
* [Digital Signatures][signatures]: sign messages with a private key which can
  be verified by a public one
* [Authenticators][macs]: create codes which can be used to check the
  authenticity of messages
* [Hash Functions][hashes]: compute a secure, fixed-length code from a message
  which does not reveal the contents of the message

Additional power-user features are available. Please see the Wiki for further
information.

[wiki]: https://github.com/cryptosphere/rbnacl/wiki
[secretkey]: https://github.com/cryptosphere/rbnacl/wiki/Secret-Key-Encryption
[publickey]: https://github.com/cryptosphere/rbnacl/wiki/Public-Key-Encryption
[signatures]: https://github.com/cryptosphere/rbnacl/wiki/Digital-Signatures
[macs]: https://github.com/cryptosphere/rbnacl/wiki/Authenticators
[hashes]: https://github.com/cryptosphere/rbnacl/wiki/Hash-Functions

## Security Notes

NaCl itself has been expertly crafted to avoid a whole range of
side-channel attacks, however the RbNaCl code itself has not been
written with the same degree of expertise. While the code is
straightforward it should be considered experimental until audited
by professional cryptographers.

That said, it's probably still a million times better than OpenSSL...

## Learn More

While NaCl has designed to be easier-than-usual to use for a crypto
library, cryptography is an incredibly difficult subject and it's
always helpful to know as much as you can about it before applying
it to a particular use case. That said, the creator of NaCl, Dan
Bernstein, has published a number of papers about NaCl. If you are
interested in learning more about how NaCl works, it's recommended
that you read them:

* [Cryptography in NaCl](http://cr.yp.to/highspeed/naclcrypto-20090310.pdf)
* [Curve25519: new Diffie-Hellman speed records](http://cr.yp.to/ecdh/curve25519-20060209.pdf)
* [Ed25519: High-speed high-security signatures](http://ed25519.cr.yp.to/ed25519-20110926.pdf)

Have a general interest in cryptography? Check out the free course
Coursera offers from Stanford University Professor Dan Boneh:

[http://crypto-class.org](http://crypto-class.org)

## Contributing

* Fork this repository on Github
* Make your changes and send a pull request
* If your changes look good, we'll merge 'em

## License

Copyright (c) 2013 Tony Arcieri, Jonathan Stott.
Distributed under the MIT License. See LICENSE.txt for further details.
