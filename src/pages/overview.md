---
layout: ../layouts/Layout.astro
title: Overview
---

# Overview

The Autograph protocol allows one party (”Bob”) to cryptographically verify any
type of data from another party (”Alice”) based on public keys and signatures
from trusted third parties (e.g. ”Charlie”).

## Preliminaries

### Roles

![](/images/parties.png)

The Autograph protocol typically involves three parties: **Alice**, **Bob**,
**Charlie**.

- **Alice** wants to send encrypted data to Bob and certify that she is the
  owner of the data.
- **Bob** wants to accept encrypted data from parties like Alice and verify its
  ownership. To enable this scenario, Bob relies on cryptographic signatures
  from trusted third parties like Charlie.
- **Charlie** creates cryptographic signatures that certifies ownership of data
  for parties like Alice. Charlie is trusted by both Alice and Bob. This allows
  Bob to verify the ownership of data that he receives from Alice.

### Keys, signatures & data

![](/images/keys-signatures-data.png)

- An **Identity key** is used to cryptographically identify a party.
- **Signatures** are used to cryptographically verify ownership and integrity of
  a party's identity key and data.
- **Certificates** contain pairs of identity keys and signatures from third
  parties that have verified the ownership and integrity of a party's identity
  key and data.
- A list of identity keys from **trusted parties** can be used verify that one
  or more certain third parties have verified the ownership and integrity of a
  party's identity key and data.
- The integrity and ownership can be verified for any type of **data**.
- Single-use, **ephemeral keys** are used to derive keys for encryption and
  prevent [replay attacks](https://en.wikipedia.org/wiki/Replay_attack).

## The protocol

![](/images/flow.png)

Autograph can be divided into the following steps:

1. **Establish trust**: Bob and Charlie mutually authenticate each other. Bob
   adds Charlie as a trusted party.
2. **Certifiy ownership**: Alice and Charlie mutually authenticate each other.
   As part of the authentication process Alice may include additional data that
   she owns. Charlie creates a signature that certifies Alice's ownership of her
   cryptographic identity and data. Alice adds the signature and Charlie's
   public key to a certificate.
3. **Verify ownership**: Alice authenticates with Bob. She includes the
   certificate from above. Since Charlie is one of Bob's trusted parties, Bob
   can verify Alice's ownership of her cryptographic identity and data without
   further contact with Charlie.

### Authentication

![](/images/auth.png)

To authenticate, a party will create an encrypted message. This message will be
used to:

- Verify that they are in control of their private identity key.
- Verify the integrity of the data.
- Verify that the desired number of trusted third parties, if any, have verified
  the ownership of their identity key and data.

To create the authentication message, a party will:

- **Sign** the other party's ephemeral public key and their own data. The
  resulting signature certifies the integrity of the data, that they are in
  control of their identity private key, and that it's not a replay attack.

- **Encrypt** the signature from above, a certificate containing pairs of
  identity keys and signatures from third parties, and the data itself.

### Step 1: Establish trust

![](/images/trust.png)

Bob and Charlie mutually authenticate each other. Bob adds Charlie as a trusted
party.

### Step 2: Certify ownership

![](/images/certify.png)

Alice and Charlie mutually authenticate each other. Charlie creates a signature
that certifies Alice's ownership. Alice adds the signature and Charlie's public
key to a certificate.

### Step 3: Verify ownership

![](/images/verify.png)

Alice authenticates with Bob using the certificate with Charlie's public key and
signature. Bob can verify Alice's ownership without further contact with
Charlie.

## Learn more

[Read the full specification &rarr;](/docs/specification)
