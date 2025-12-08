+++
title = "Network Security and TLS - Course Notes"
date = "2025-12-08"
author = "Max"
tags = ["network", "security", "TLS", "encryption", "cryptography"]
description = "Notes covering network security principles, encryption, and TLS protocol"
+++

## Network Security

1. confidentiality: unable to read (encrytion)
2. integrity: no injection
3. availability: shouldn't prevent communication access (DoS/DDoS)

network security exists at top layers mostly(because imagine lower layer like wire, should be hard to be attacked. and communication security should be crucial for wireless medium, I assumed)

Access control:
1. something you have like DUO app
2. something you know like password
3. something you are like fingerprints

trends: multi-factor authentication

Encryption Basics:
1. symmetric: same key for encoding and decoding(AES)
2. asymmetric: different key for encoding and decoding(RSA)
Integrity:
Hash function -> secure hash algorithm(SHA)

Attacks:
1. eavesdropping: intercept messages
2. insertion
3. hijacking

Public key Cryptography: public key, private key

TLS: widely deployed on the web(actually a application layer protocol)
1. Alice send message to Bob
2. Bob use private key to generate message(digital signature)
3. Alice received and use public key(certificate authorities) to verify it is Bob's signature
4. Bob and Alice exchange a symmetric session key Ks, Alice use public key to encrypt and only Bob have the private key to decrypt the key
5. then use symmetric key crpytography(AES) to encrypt messages
RSA is much slower than AES, the computational expense.
