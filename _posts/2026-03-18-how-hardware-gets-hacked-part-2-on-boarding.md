---
layout: post
title: "How Hardware Gets Hacked (Part 2): On-boarding"
date: 2026-03-18
type: article
subjects:
  - security
  - education
excerpt: >
  Part 2 rebuilds the eCTF project in four progressive builds — simulator, test
  commands, real hardware, automated tests — and examines what information
  attackers can and cannot see during the build process.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-2-on-boarding).*

![Hardware testing setup for the HHGH project]({{ '/assets/hhghp2/hardware_testing.png' | relative_url }})

The 2023 MITRE eCTF required specific hardware and MITRE's own bootloader. Part 2 re-builds the same car-and-key-fob project in a form you can run on your own development boards, structured as four progressive builds: a pure host simulation (no hardware required), the simulation extended with interactive test commands, a build targeting real STM32 and TM4C hardware, and a build with an automated test suite for black-box testing.

The more security-relevant half of the article examines the secret-generation pipeline. Two generation steps occur: a global step before any device is built (the right place for system-wide AES keys) and a per-device step when each car or fob is compiled, producing `secrets.h` and `car_secrets.json`. Competition rules give attackers full access to source code and build scripts but not to build artifacts — they can read `car_gen_secret.py` but not the secrets it generates. Whether they can infer the contents of `secrets.h` from the visible script alone is a question worth asking before the attack phase begins.

[Read the full article →](https://www.digikey.com/en/maker/blogs/2026/how-hardware-gets-hacked-part-2-on-boarding)
