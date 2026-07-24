---
layout: post
title: "How Hardware Gets Hacked: Authenticated Exchanges (Teardown 2026)"
date: 2026-07-24
type: tutorial
subjects:
  - security
  - firmware
venue: Crowd Supply Teardown
excerpt: >
  Workshop materials from Teardown Portland 2026: building up a badge-and-reader
  access control system from a bare UID check to mutual authentication with
  derived keys and session keys, one broken assumption at a time.
documents:
  - title: "Workshop Worksheet (PDF)"
    url: /assets/teardown26_authenticated_exchanges/worksheet.pdf
    type: pdf
  - title: "Slides (PDF)"
    url: /assets/teardown26_authenticated_exchanges/authenticated_exchanges.pdf
    type: pdf
---

*Workshop given at [Teardown Portland 2026](https://www.crowdsupply.com/teardown/portland-2026/workshop/how-hardware-gets-hacked-authenticated-exchanges), July 2026.*

![Sequence diagram of mutual authentication between a badge and a door reader, alongside a passing test log showing both phases of the handshake succeeding]({{ '/assets/teardown26_authenticated_exchanges/mutual_authentication.png' | relative_url }})

Code and exercises for this workshop are on GitHub: [nathancharlesjones/authenticated_exchanges](https://github.com/nathancharlesjones/authenticated_exchanges).

Authentication is one of five foundational security principles — alongside confidentiality, integrity, availability, and non-repudiation — and it's the one this workshop dug into: how do you prove a message or piece of data actually came from who it claims to have come from? The running example is a physical access control system: badges and a reader attached to a door. Each exercise breaks a specific assumption in the previous defense, and the fix that follows repairs it.

**Baseline: the UID allowlist**

The starting point is about as simple as authentication gets. A badge presents its ID number; the reader checks it against an allowlist and opens the door if it matches. The "secret" here is just the badge's UID, and in a non-adversarial world that's a fine secret to share in the clear — much like typing a password on a keyboard is fine when you can safely assume an attacker isn't watching. The assumption breaks the moment an attacker can observe traffic, guess a UID, or pull one out of a firmware image or a public repo.

**First defense: challenge-response**

Once the UID itself can leak, sending it directly is no longer sufficient — we need to prove knowledge of a secret without transmitting it, and without letting an attacker learn anything usable even after watching many exchanges. That's what a **message authentication code (MAC)** buys us: the reader sends a nonce, the badge computes a MAC over it with a shared key, and only a badge holding the correct key can produce the right response. This introduces its own new assumptions — the badge can do the computation, the debug port is locked, firmware updates arrive securely — and raises the question of where a good nonce comes from in the first place (PRNG vs. TRNG, and the tradeoffs of each).

**Second defense: per-device keys**

A single shared MAC key across an entire fleet of badges creates a blast-radius problem: steal one badge, dump its firmware or brute-force query it, and the whole fleet is compromised. The fix is deriving a unique device key per badge — `HMAC(fleet_key, UID)` — so the reader never has to store thousands of individual keys but can still recompute the right one on the fly. Losing one badge now only costs one key, provided it gets revoked before an attacker can use it. This is also where key management stops being an afterthought: how a key is generated at the factory, how it's stored on-device, when and how it's used, and how it gets revoked all become load-bearing questions.

**Third defense: mutual authentication**

Every defense so far only authenticates the badge to the reader — nothing stops a skimmer or a rogue reader from "authenticating" a badge and then reading or writing its private data. The fix is to flip the check around: the reader also has to prove who it is before the badge will let it touch anything sensitive. That means moving to asymmetric cryptography and digital signatures, since a shared secret that every reader needs to know is just another thing an attacker can extract from a stolen badge. This is the exercise shown in the diagram above: the badge authenticates to the reader as before, then the reader signs a badge-supplied nonce with its private key, which the badge verifies against a known public key.

**Fourth defense: session keys**

Even after mutual authentication, an attacker who can observe or intercept the conversation can still read or tamper with the data exchanged afterward. The final piece derives a session key — using the same fleet-key-plus-UID derivation trick as before, with an info string to separate it from the device key — so that traffic after the handshake is encrypted with a key that isn't the long-lived device key and doesn't threaten forward secrecy if it's ever exposed.

**What's still open**

The workshop closes on the questions it deliberately left out: authorization (what a badge is allowed to do once authenticated), what happens when a reader's public key isn't known in advance, resource constraints on real hardware, and how to handle failures — logging, lockouts, and lengthening timeouts — without those becoming a denial-of-service vector of their own. Every defense here closes off one avenue while relying on a fresh assumption of its own; the interesting part of security engineering is knowing what those assumptions are and deciding, deliberately, which ones you're willing to make.

**Additional Resources**

- [How Hardware Gets Hacked (Part 6): Authenticated Exchanges]({% post_url 2026-07-06-how-hardware-gets-hacked-part-6-authenticated-exchanges %}) — the eCTF key fob replaces its broken PRNG-based unlock with a rolling counter and AES-CMAC, the same MAC-based authentication idea applied to a real embedded target
- [GitHub repo →](https://github.com/nathancharlesjones/authenticated_exchanges) — all five exercises, tests, and the worksheet

[Session page →](https://www.crowdsupply.com/teardown/portland-2026/workshop/how-hardware-gets-hacked-authenticated-exchanges)
