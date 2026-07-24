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

**Five defenses, each closing off the last attack**

- **Baseline: the UID allowlist** — A badge presents its ID number; the reader checks it against an allowlist and opens the door if it matches. Fine when an attacker can't observe traffic or guess a UID — broken the moment one leaks from a log, a firmware image, or a public repo.
- **Challenge-response** — The reader sends a nonce and the badge computes a **message authentication code (MAC)** over it with a shared key, proving knowledge of a secret without ever transmitting it. This raises new questions of its own, like where a good nonce comes from (PRNG vs. TRNG).
- **Per-device keys** — A single MAC key shared fleet-wide means one stolen badge compromises everyone. Deriving a unique device key per badge — `HMAC(fleet_key, UID)` — caps the blast radius to one badge and makes key management (generation, storage, revocation) a first-class concern.
- **Mutual authentication** — Nothing so far stops a rogue reader from "authenticating" a badge and reading its private data. The reader now has to prove itself too, using asymmetric cryptography and digital signatures so no shared secret sits on the reader side waiting to be extracted.
- **Session keys** — Even after mutual authentication, an eavesdropper can still read the traffic that follows. A session key, derived the same way as the device key but tagged with an info string, encrypts post-handshake traffic without touching the long-lived device key or forward secrecy.

**What's still open**

The workshop closes on the questions it deliberately left out: authorization (what a badge is allowed to do once authenticated), what happens when a reader's public key isn't known in advance, resource constraints on real hardware, and how to handle failures — logging, lockouts, and lengthening timeouts — without those becoming a denial-of-service vector of their own. Every defense here closes off one avenue while relying on a fresh assumption of its own; the interesting part of security engineering is knowing what those assumptions are and deciding, deliberately, which ones you're willing to make.

**Additional Resources**

- [How Hardware Gets Hacked (Part 6): Authenticated Exchanges]({% post_url 2026-07-06-how-hardware-gets-hacked-part-6-authenticated-exchanges %}) — the eCTF key fob replaces its broken PRNG-based unlock with a rolling counter and AES-CMAC, the same MAC-based authentication idea applied to a real embedded target
- [GitHub repo →](https://github.com/nathancharlesjones/authenticated_exchanges) — all five exercises, tests, and the worksheet

[Session page →](https://www.crowdsupply.com/teardown/portland-2026/workshop/how-hardware-gets-hacked-authenticated-exchanges)
