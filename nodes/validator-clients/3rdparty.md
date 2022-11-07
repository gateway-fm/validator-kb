# Vouch + Dirk

### [Vouch](https://github.com/attestantio/vouch) 

Vouch is a multi-node highly-available validator client, developed by
Attestant. It allows to use multiple nodes at once to make sure that your
system is always as available and as efficient as possible.

It has a relatively steep learning curve, but it is very flexible in its
configuration.

## External Signer / Wallet

The biggest risk of running a validator client is keys being lost or stolen. To
improve security over that, it is advised to not keep the keys on the
nodes/validator clients, but instead use a separate client, so-called "externa"
or "remote" signer. That allows for better separation of responsibilities, and
for smaller attach surface, because only the machine with the keys needs most
protection.

### [Dirk](https://github.com/attestantio/dirk)

Supported by Vouch. Dirk is a very comprehensive external signer, with
[extensive system of permissions](https://github.com/attestantio/dirk/blob/master/docs/permissions.md)
and using TLS for both authentication and encryption.

It also supports [distributed key generation and signing](https://github.com/attestantio/dirk/blob/master/docs/distributed_key_generation.md),  making the system more highly available and secure.

The biggest downside is that it has a steep learning curve and also it supports
only Vouch as a validator client.

* [Getting Started With
    Dirk](https://github.com/attestantio/dirk/blob/master/docs/getting_started.md)

