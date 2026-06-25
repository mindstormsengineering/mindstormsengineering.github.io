---
layout: post
title: "All Your Bytes are Belong to Us"
date: 2025-12-01
type: article
subjects:
  - security
venue: DigiKey
excerpt: >
  A survey of hardware attack techniques organized as six levels of cost and
  invasiveness — from researching a device online to decapping its IC and editing
  the silicon with a focused ion beam.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/blogs/2025/all-your-bytes-are-belong-to-us).*

![Hardware attack spectrum from passive reconnaissance to IC modification]({{ '/assets/images/spectrum.png' | relative_url }})

Network security gets most of the attention, but every electronic device that someone can physically touch is also susceptible to hardware attacks — including devices with no wireless radios at all. This article surveys what those attacks look like, organized into six ascending levels of cost, skill, and invasiveness.

Level 1 is reconnaissance: reading datasheets, finding reverse-engineering projects, studying the PCB. Level 2 is snooping: listening on UART, SPI, JTAG, or I2C with a logic analyzer. Level 3 is PCB modification: cutting traces, adding wires, replacing components. Level 4 is side-channel attacks: inferring secrets from timing, power consumption, or electromagnetic emissions — no physical modification required. Level 5 is fault injection: inducing computational errors through voltage glitching, EMFI, or lasers to skip instructions or corrupt memory. Level 6 is IC decapping: removing the chip's packaging to expose the silicon die, enabling photonic side-channel analysis, optical fault injection, or direct circuit modification with a focused ion beam (FIB).

The takeaway isn't that all devices need to defend against all six levels — it's that the right level of protection depends on what you're protecting and who's likely to attack it. Countermeasures exist for every level; a device only needs to be secure enough for its actual threat model.

**Additional Resources**

- [Nothing is Safe (JawnCon 0x2)]({% post_url 2025-10-10-jawncon26-nothing-is-safe %}) — a talk covering the same attack spectrum with live demonstrations of DPA and fault injection
- [How Hardware Gets Hacked →](https://www.digikey.com/en/maker/search-results?t=Nathan%20Jones%20How%20Hardware%20Gets%20Hacked&f=1981359301) — a multi-part series walking through a complete attack and defense, from start to finish

[Read the full article →](https://www.digikey.com/en/maker/blogs/2025/all-your-bytes-are-belong-to-us)
