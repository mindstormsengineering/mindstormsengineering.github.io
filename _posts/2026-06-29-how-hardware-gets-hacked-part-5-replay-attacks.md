---
layout: post
title: "How Hardware Gets Hacked (Part 5): Replay Attacks"
date: 2026-06-29
type: article
subjects:
  - security
venue: DigiKey
excerpt: >
  Exploiting the eCTF key fob's completely unauthenticated unlock message via
  a literal replay attack, then building — and breaking — a PRNG-based defense
  that looks secure right up until an attacker intercepts three messages.
documents:
  - title: "Replay Attacks (PDF)"
    url: /assets/hhghp5/hhghp5_replay-attacks.pdf
    type: pdf
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-5).*

![Recording a fob's unlock transmission with a logic analyzer and replaying it to a car with a pin wiggler]({{ '/assets/hhghp5/hhghp5_04_replay-atk-diagram_300.png' | relative_url }})

Part 5 attacks the eCTF key fob's unlock message directly: `[ 0x56 | 0x6 | "unlock" ]`, sent verbatim over UART with no authentication whatsoever. There are three ways to exploit it: construct the message from scratch and send it over a USB-to-UART adapter, record a real fob's transmission with a logic analyzer and replay the exact bit pattern with a pin wiggler, or just walk up with any paired fob, since every car accepts the same static password. All three unlock every car in the fleet.

The article uses this to introduce **authenticity** — the property that lets a receiver verify who actually sent a message — and separates it from confidentiality (can an attacker read the message?) and integrity (can an attacker modify it?). The car doesn't need either of those two; it needs a way to know an unlock message truly came from a paired fob, over a channel where an attacker can see everything that crosses the wire.

The first fix attempted is an LCG/PRNG: seed and constants generated randomly at build time, with each unlock message carrying the next pseudo-random value in a shared sequence instead of the static password. It resists naive replay (the car rejects stale values) and never reveals the seed or constants directly. But it's a **near miss**: because a linear congruential generator is, well, linear, an attacker who intercepts just three consecutive unlock messages has three equations and three unknowns — enough algebra to solve for the constants and predict every future value the fob will ever send.

The fix needs a **one-way function**, something an attacker can't invert even after watching many outputs — in other words, real cryptography, which is where the next article picks up.

[Read the full article →](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-5)
