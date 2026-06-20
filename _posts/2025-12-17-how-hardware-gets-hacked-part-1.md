---
layout: post
title: "How Hardware Gets Hacked (Part 1)"
date: 2025-12-17
type: article
subjects:
  - security
  - education
excerpt: >
  Introduction to the series: the MITRE Embedded Capture the Flag competition,
  the insecure car-and-key-fob system that serves as the target, and what flags
  are at stake across its four main operations.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/blogs/2025/how-hardware-gets-hacked-part-1).*

![Feature summary of the HHGH car-and-key-fob target system]({{ '/assets/hhghp1/hacked1_01_features.png' | relative_url }})

Hardware security is easier to learn by doing than by reading about it in the abstract. This series uses the 2023 MITRE Embedded Capture the Flag (eCTF) competition as the vehicle: a structured competition in which teams design and harden an embedded system, then spend weeks trying to extract flags — proof-of-exploitation tokens — from each other's designs.

Part 1 introduces the target: a car and key fob system with four main operations — unlock car with a paired fob, pair a new fob to a car, enable an optional feature, and package a feature onto a fob. Each operation has one or more flags that an attacker captures if they trigger it without authorization. The article walks through the insecure example MITRE provided for the 2023 competition, examining each operation's code at the source level, and sets up the rest of the series: iteratively attack the system, implement defenses, attack the updated system, and repeat.

[Read the full article →](https://www.digikey.com/en/maker/blogs/2025/how-hardware-gets-hacked-part-1)
