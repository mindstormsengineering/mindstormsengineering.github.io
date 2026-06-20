---
layout: post
title: "How Hardware Gets Hacked (Part 3): Adopting the Attacker Mindset"
date: 2026-04-20
type: article
subjects:
  - security
  - education
excerpt: >
  Part 3 is about reconnaissance: a four-step framework for building an
  attacker's understanding of the target before attempting any exploit.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-3-adopting-the-attacker-mindset).*

![Vince, the attacker persona used throughout the HHGH series]({{ '/assets/hhghp3/vince.png' | relative_url }})

Before attempting an attack, a good attacker does reconnaissance. Part 3 structures that reconnaissance into four objectives: identify the payoffs (what flags exist and where they're stored), review the overall design for known weaknesses, enumerate every attacker-controlled input into the system, and catalog potential vulnerabilities — specifically distinguishing known bugs from "interesting oddities," things in the code that are technically correct but fragile or surprising.

The article applies this framework to the insecure example's source code, surfaces a list of bugs and oddities, and explains where an attacker looks for additional design information: manufacturer datasheets and errata, maintenance and repair documentation, published reverse-engineering work, and the device's own response to probing. The resulting lists of inputs and vulnerabilities become the foundation for the prioritized attack matrix in Part 4.

[Read the full article →](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-3-adopting-the-attacker-mindset)
