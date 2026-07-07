---
layout: post
title: "How Hardware Gets Hacked (Part 6): Authenticated Exchanges"
date: 2026-07-06
type: article
subjects:
  - security
venue: DigiKey
excerpt: >
  Replacing the eCTF key fob's broken PRNG-based unlock scheme with a rolling
  counter and a real MAC — AES-CMAC — so the car can verify an unlock
  message came from a paired fob without the shared key ever crossing the
  wire.
documents:
  - title: "Authenticated Exchanges (PDF)"
    url: /assets/hhghp6/hhghp6_authenticated-exchanges.pdf
    type: pdf
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-6).*

![Unlock message built from a UNLOCK_MAGIC byte, length, fob ID, and counter, with an AES-CMAC computed over that payload and the secret key appended as the MAC]({{ '/assets/hhghp6/hhghp6_05_unlock-message-with-MAC_300.png' | relative_url }})

Part 5 ended with the fob's PRNG-based defense broken by simple algebra — a linear congruential generator turned out to be invertible from just three intercepted messages. Part 6 replaces it with real cryptography: a secret key generated at build time and embedded in both car and fob firmware, combined with a **rolling counter** that increments on every unlock attempt. Before transmitting, the fob runs its ID, the counter, and the unlock command through AES-CMAC with the shared key and appends the resulting MAC to the message.

The car doesn't need to predict anything; it recomputes the same MAC over the received fields and checks that it matches, and that the counter falls within an acceptable window of the last value it saw. A replayed message fails the counter check. A forged message fails the MAC check, because producing a valid one requires the secret key, which never travels over the wire in the clear. That's the difference between **authenticity** and mere obfuscation.

The article closes by turning the "what's still broken?" question back on the reader: counter rollover, flash wear from writing the counter on every unlock, revoking a lost or stolen fob, and capping how many fobs can pair to one car all need real answers before this ships to production.

[Read the full article →](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-6)
