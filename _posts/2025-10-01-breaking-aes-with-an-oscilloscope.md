---
layout: post
title: "Breaking AES with an Oscilloscope"
date: 2025-10-01
type: article
subjects:
  - security
  - education
excerpt: >
  A step-by-step walkthrough of differential power analysis (DPA) — using an
  oscilloscope and statistics to extract a private AES128 key from a running
  device — with practical countermeasures for engineers who need to defend
  against this class of hardware attack.
---

*Originally published on [EmbeddedRelated](https://www.embeddedrelated.com/showarticle/1761.php).*

![Differential power analysis attack traces]({{ '/assets/breaking_aes/dpa_attack.png' | relative_url }})

Network security gets most of the attention in embedded systems security discussions, but physical access attacks are equally dangerous — and far less well understood. This article tackles one concrete example: differential power analysis (DPA), a technique that uses an oscilloscope to extract a private AES encryption key from a device that the attacker can interact with but whose ciphertext they cannot observe. The attack exploits the fact that a processor's power consumption varies depending on the data being processed and the operations being performed — and that this variation is measurable.

By sending a carefully chosen set of plaintexts to the target device and measuring the power trace for each encryption, an attacker can use statistical correlation to tie specific power patterns to specific key bytes. Repeating this across all 16 key bytes recovers the full AES128 key in minutes, using nothing more exotic than an oscilloscope and some math. The article walks through the complete setup, the measurement methodology, and the correlation analysis with enough detail to follow along or replicate it.

The final section covers the countermeasures that actually work: adding noise to power consumption, inserting random delays between operations, masking the intermediate AES values to decorrelate the power signal from the key, or using a hardware AES accelerator designed to resist power analysis. A practical companion to the more theoretical treatment of hardware security — and a useful reminder that encryption is not the same as security.

[Read the full article →](https://www.embeddedrelated.com/showarticle/1761.php)
