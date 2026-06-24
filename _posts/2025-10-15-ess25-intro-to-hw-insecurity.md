---
layout: post
title: "An Introduction to Hardware (In)Security with the ChipWhisperer-Nano (Embedded Systems Summit 2025)"
date: 2025-10-15
type: tutorial
subjects:
  - security
  - hardware
  - education
excerpt: >
  Workshop slides from Embedded Systems Summit 2025: hands-on differential power
  analysis and fault injection using the ChipWhisperer Nano.
documents:
  - title: "Slides (PDF)"
    url: /assets/ess25_intro_to_hw_insecurity/Introduction-to-HW-Insecurity_Nathan-Jones.pdf
    type: pdf
---

*Workshop given at [Embedded Systems Summit 2025](https://embeddedsummit.com/index_2025.php#speakers-title), October 2025.*

The Embedded Systems Summit draws a production-firmware crowd, which makes the hardware security workshop land differently than it does at a maker event. There's less "wait, you can do that?" and more "okay, how do I design against it?" That's a great room to teach in.

The workshop ran in three parts: situating hardware attacks within the broader attack sequence, a hands-on differential power analysis attack on AES using the ChipWhisperer Nano, and a fault injection demonstration. If you had a ChipWhisperer Nano, you could follow along live; if not, I provided pre-collected datasets so you could still work through the exercises.

**The hardware attack sequence**

Before the hands-on material, I framed DPA and fault injection within the broader context of how hardware attacks typically unfold — from reconnaissance (datasheets, teardowns, PCB photos) through interface snooping and hardware modification, on up to side-channel analysis and fault injection. Understanding this sequence helps engineers know where to invest defensive effort. Most successful attacks don't start with an oscilloscope; they start with a publicly available datasheet.

**Differential power analysis on AES**

The main event was a DPA attack on a target microcontroller running AES. The ChipWhisperer Nano captures power traces while the target encrypts known plaintexts. The attack exploits the Hamming weight model: the power consumed during an operation correlates with the number of set bits in the intermediate result. By grouping traces according to a predicted bit of the S-box output for each key byte guess, averaging, and subtracting, a peak appears at the computation moment when the key guess is correct — and washes out for wrong guesses.

We worked through this in Jupyter notebooks, building up from plotting individual traces to running the full attack. Watching attendees get their first peak above the noise is one of my favorite parts of teaching this material.

**Fault injection**

For the final section, I demonstrated a voltage glitching attack to bypass a password check. A brief drop on the supply rail, timed precisely to the branch instruction enforcing the comparison, causes the device to skip it and grant access without knowing the password. The ChipWhisperer Nano provides hardware trigger support for nanosecond-level precision. It's a viscerally convincing demonstration of why "lock your debug port" is only the beginning.

**The takeaway**

These attacks are real and accessible. A ChipWhisperer Nano costs around $50. The defense isn't helplessness — it's intentionality. Constant-time comparisons, locked debug ports, secure boot, and randomized execution delays are all within reach. The key is treating security as a design criterion from the start, not a retrofit.

**Additional Resources**

- [Introduction to Hardware (In)Security with the ChipWhisperer-Nano (EOC 2026)]({% post_url 2026-05-14-eoc26-intro-to-hw-insecurity %}) — the same workshop with a full recording and exercise files

[Session page →](https://embeddedsummit.com/index_2025.php#speakers-title)
