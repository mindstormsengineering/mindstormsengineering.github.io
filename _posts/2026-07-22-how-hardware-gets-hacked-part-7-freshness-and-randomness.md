---
layout: post
title: "How Hardware Gets Hacked (Part 7): Freshness and Randomness"
date: 2026-07-22
type: article
subjects:
  - security
venue: DigiKey
excerpt: >
  Breaking the eCTF key fob's rolling-counter-plus-MAC defense with RollJam,
  forced rollback, and forced rollover attacks, then closing the gap with a
  challenge-response nonce scheme and a PRNG seeded from real hardware entropy.
documents:
  - title: "Freshness and Randomness (PDF)"
    url: /assets/hhghp7/hhghp7_freshness_and_randomness.pdf
    type: pdf
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-7-freshness-and-randomness).*

![RollJam attack sequence: an attacker intercepts each unlock message from a fob, forwards the previous message to the car, and keeps one unused valid message in reserve to unlock later]({{ '/assets/hhghp7/hhghp7_02_rolljam_diagram_300.png' | relative_url }})

Part 6 closed the door on naive replay with a rolling counter and an AES-CMAC. Part 7 shows the door was only half-shut: three more sophisticated attacks still let an attacker replay a stale message. **RollJam** intercepts every unlock attempt, forwards the second-most-recent message to the car while banking the newest one for later use. **Forced rollback** re-flashes the car's firmware to reset its stored counter to zero, resurrecting an old captured message. **Forced rollover** just triggers enough unlocks (up to 65,536 for a 16-bit counter) to wrap the counter back around to a value an old message still satisfies. All three exploit the same gap: the scheme proves a message came from an authenticated fob *at some point in the past*, never that it was generated *right now*.

That distinction — between authenticity and freshness — matters differently depending on what's being verified. A signed firmware update is fine no matter how old it is; the signature alone proves authenticity. A live "unlock" command isn't, because an attacker watching the wire can capture and hold a genuinely valid message and nothing about it says when it happened. The fix is challenge-response: the car generates a random value (a "nonce," a **n**umber used **once**) and asks the fob to compute a MAC over it. Since the fob can't know the nonce until the car sends it, a correct response proves the fob is answering *this* conversation, not replaying pieces of a previous one.

That scheme is only as strong as the nonce generator behind it. A naive LCG-style `rand()` is out — Part 5 already showed one is invertible from three intercepted outputs. Instead, the article reuses AES-CMAC itself as a one-way PRNG (the same construction NIST recommends for CTR-DRBG), driven by a key kept separate from the unlock key through key separation. That still leaves one gap: if the PRNG always starts from the same internal state, an attacker who can reset the device sees the identical "random" sequence every time. Closing it means seeding the PRNG from actual hardware noise — RAM startup values, clock jitter, ADC readings on Vcc, temperature, and a floating pin — accumulated into an entropy pool and measured for real using NIST's SP800-90B toolkit rather than assumed.

The article closes with a look at what else could get you there: TOTP (if fob and car can keep synchronized time), rate-limiting unlock attempts, a hardware anti-rollback counter, or an MCU with a built-in TRNG — each a different way of buying the same property the whole article is really about: proving a message is fresh, not just authentic.

[Read the full article →](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-7-freshness-and-randomness)
