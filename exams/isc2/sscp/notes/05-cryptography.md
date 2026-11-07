---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 12 min
---

# 05 - Cryptography

**Domain 5: Cryptography (9%)** - objectives 5.1 to 5.4.

The smallest domain, and the one candidates fear most. It is learnable because the exam asks what each tool is for, not how the mathematics works.

---

## 5.1 Reasons and requirements

Cryptography provides **confidentiality** (encryption), **integrity** (hashing, MACs), **authentication** and **non-repudiation** (digital signatures). Choose it by what you need to protect and why: data classification, legal requirements for protecting personal or payment data, and where the data sits. Data **at rest** (disks, databases, backups), **in transit** (networks) and **in use** (memory) each need a plan; the third is the hardest and is where hardware enclaves help.

**Quantum concepts** matter for planning. A sufficiently powerful quantum computer would break today's public key algorithms (the ones based on factoring and discrete logarithms), while symmetric algorithms and hashes are weakened but survive with larger sizes. Adversaries can record encrypted traffic today and decrypt it later, so long-lived secrets are at risk first. NIST has standardised post-quantum algorithms; FIPS 203 (August 2024) specifies ML-KEM, a key-encapsulation mechanism meant to resist quantum attack, in three parameter sets (ML-KEM-512, -768 and -1024). For the exam: know the problem and that the answer is migration to post-quantum algorithms, supported by good **crypto-agility**, meaning the ability to swap algorithms without redesigning systems.

## 5.2 Cryptography concepts

**Symmetric encryption** uses one shared key for both directions. It is fast and suits bulk data, but the key distribution problem is hard: how do you get the key to the other side safely? AES, specified in FIPS 197, is the standard: a 128-bit block cipher with key sizes of 128, 192 and 256 bits. Key length is the number that grows strength; a longer key means more brute-force work.

**Asymmetric encryption** uses a mathematically linked pair: a public key anyone can have and a private key only the owner holds. It solves distribution but is slow, so real systems use it to agree or wrap a symmetric key and then use the symmetric key for the data. This hybrid pattern is behind TLS. Remember the direction of use:

| Goal | Encrypt or sign with | Verify or decrypt with |
|---|---|---|
| Confidentiality to Alice | Alice's public key | Alice's private key |
| Digital signature by Alice | Alice's private key | Alice's public key |

**Hashing** turns any input into a fixed-size digest. It is one-way, and a good hash makes changing the input change the digest unpredictably and makes finding two inputs with the same digest (a **collision**) infeasible. Use hashes for integrity checks and for storing password verifiers. A hash is not encryption and cannot be reversed. Passwords should be hashed with a slow, purpose-built password hashing function and a unique **salt** per user: a salt is random data mixed in so identical passwords produce different hashes and precomputed (rainbow) tables fail. A **pepper** is a secret kept outside the database.

**Digital signatures** hash the message and sign the hash with a private key, giving integrity, authentication and non-repudiation together. A **message authentication code (MAC)** also gives integrity and authenticity, but with a shared key, so it cannot give non-repudiation: either party could have produced it.

Strength depends on the algorithm, key length and implementation. **Cryptanalysis** is the study of breaking systems, including brute force, known-plaintext and side-channel attacks, and most real failures come from poor key handling or implementation, not broken mathematics. Never invent your own algorithm; use vetted ones.

## 5.3 Secure protocols

Match the protocol to the use case, and know the weak ones to retire.

- **TLS** secures web and many other connections. TLS 1.3 (RFC 8446, August 2018) is designed to prevent eavesdropping, tampering and message forgery; the RFC page now marks it as superseded by RFC 9846, so check the current document, but the exam principle is unchanged: use current TLS and disable old SSL and early TLS versions.
- **HTTPS** is HTTP over TLS. **SSH** replaces Telnet for remote administration. **SFTP** and **SCP** replace FTP.
- **IPsec** secures traffic at the network layer, in transport mode (host to host, payload protected) or tunnel mode (gateway to gateway, whole packet protected). It uses **IKE** to negotiate keys and the **AH** and **ESP** protocols, where ESP gives encryption and AH only integrity.
- **S/MIME** and **PGP** protect email content; **DNSSEC** adds signatures so DNS answers can be verified (integrity, not confidentiality).
- **Limitations**: a protocol that encrypts the channel does not protect the data once it arrives, and weak ciphers or expired certificates quietly undo the benefit.

## 5.4 Public key infrastructure

PKI binds public keys to identities using **certificates**. A **certificate authority (CA)** signs certificates after a **registration authority** verifies the requester. A certificate contains the subject, the public key, validity dates and the issuer's signature; browsers and operating systems trust a set of root CAs, and trust flows down a **chain** from root through intermediate CAs. Roots are kept offline and rarely used.

When a certificate must be withdrawn before expiry, the CA publishes it on a **certificate revocation list (CRL)**, or answers status queries over **OCSP**. Checking revocation is what makes a stolen key stop working.

**Key management** is where PKI succeeds or fails. NIST SP 800-57 Part 1 Rev. 5 covers general key management best practice: the protection each key type needs and the functions involved in managing keys. A key goes through generation, distribution, storage, use, rotation, archival and destruction. Generate keys with good randomness, protect them in a **hardware security module** or a managed key service, separate duties around them, limit usage periods, back them up securely, and destroy them when retired. **Key escrow** lets a trusted party hold a copy for recovery. The **web of trust** is the alternative to CAs, used by PGP, where users vouch for each other's keys.

---

## Key terms

- **Symmetric encryption** - encryption in which the same secret key encrypts and decrypts
- **Asymmetric encryption** - encryption using a linked public and private key pair
- **Hybrid encryption** - using asymmetric cryptography to exchange a key and symmetric cryptography to protect the data
- **Hash function** - a one-way function that turns any input into a fixed-size digest
- **Collision** - two different inputs producing the same hash digest
- **Salt** - random per-user data mixed into a password before hashing so identical passwords differ and precomputed tables fail
- **Digital signature** - a hash signed with a private key, giving integrity, authentication and non-repudiation
- **Message authentication code** - a keyed checksum giving integrity and authenticity but not non-repudiation
- **Crypto-agility** - the ability to replace cryptographic algorithms without redesigning the system
- **Certificate authority** - a trusted party that signs certificates binding public keys to identities
- **Certificate revocation list** - a CA-published list of certificates withdrawn before their expiry
- **Hardware security module** - tamper-resistant hardware that generates and stores keys and performs cryptographic operations
- **Web of trust** - a decentralised model in which users vouch for one another's public keys

---

## Related

- [Notes 06: network and communications security](./06-network-and-communications-security.md)
- [TLS and HTTPS](../../../../learn/concepts/tls-and-https.md)
- **[📖 NIST FIPS 197: Advanced Encryption Standard](https://csrc.nist.gov/pubs/fips/197/final)** - AES-128, AES-192 and AES-256 with 128-bit blocks
- **[📖 NIST FIPS 203: ML-KEM](https://csrc.nist.gov/pubs/fips/203/final)** - the post-quantum key-encapsulation standard (August 2024)
- **[📖 RFC 8446: TLS 1.3](https://www.rfc-editor.org/rfc/rfc8446)** - the TLS 1.3 specification; the page notes it is superseded by RFC 9846
- **[📖 NIST SP 800-57 Part 1 Rev. 5: Key Management](https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final)** - general key management guidance
