---
layout: post
title: "How Hardware Gets Hacked (Part 4): Memory Protections"
date: 2026-05-20
type: article
subjects:
  - security
  - embedded
  - education
excerpt: >
  The first complete attack/defense cycle in this eCTF series: reading device
  secrets over an unlocked debug port, disabling it, and formalizing what was
  learned as a threat model — including what's explicitly out of scope.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-4-memory-protections).*

![Threat model for Attack #1: reading flags over an unlocked debug port]({{ '/assets/hhghp4/hhghp4-read-debug-port.png' | relative_url }})

Part 4 of "How Hardware Gets Hacked" works through the first complete attack/defense cycle. The attack: connect a debug adapter to the JTAG/SWD pins, start a GDB server, and read flags directly from flash or EEPROM — all of them, in seconds, on any unprotected device. If the secrets aren't at a known address, the article covers finding them systematically: MAP file first, then a full flash dump scanned with `strings`/`grep`, then Ghidra as a last resort.

The defense is chip-specific: RDP Level 1 on the STM32 (faults any debug flash access), DBG bits of BOOTCFG on the TM4C (disables the port outright). One notable pitfall: remapping debug pins to GPIO in firmware does *not* work — a debug adapter can reset the chip and connect before the remap runs. The unlock procedure on both chips triggers a mass erase, so an attacker can't simply unlock a locked device to extract the secrets.

The article introduces **attack-driven development (ADD)** as an organizing principle: only implement a defense when you can demonstrate the attack it prevents. The threat model at the end formalizes this — attacker profile, secrets at stake, attacks in and out of scope (SEM decapping is real but out of reach for a student competition), and the first committed defense.

The two rules to walk away with: **never distribute plaintext binaries containing secrets**, and **never ship with the debug port unlocked**.

[Read the full article →](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-4-memory-protections)
