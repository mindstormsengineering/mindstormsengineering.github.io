---
layout: post
title: "Nothing Is Safe: An Introduction to Hardware (In)Security (Teardown 2026)"
date: 2026-07-25
type: talk
subjects:
  - security
  - hardware
venue: Crowd Supply Teardown
excerpt: >
  Slides from Teardown Portland 2026: a tour of an attacker's menu of options
  against physical hardware, from a free datasheet read to focused ion beam
  edits on bare silicon.
documents:
  - title: "Slides (PDF)"
    url: /assets/teardown26_nothing_is_safe/nothing_is_safe.pdf
    type: pdf
---

*Talk given at [Teardown Portland 2026](https://www.crowdsupply.com/teardown/portland-2026/long-talk/nothing-is-safe-an-introduction-to-hardware-in-security), July 2026.*

![Hand-drawn notes on fault injection techniques (clock glitching, voltage glitching, EMFI, laser fault injection) alongside a diagram of the cryptographic model extended with side-channel leakage paths]({{ '/assets/teardown26_nothing_is_safe/summary_graphic.png' | relative_url }})

Every device that someone can physically get their hands on is a hardware security problem, whether or not it has a radio. The question worth asking isn't "if" someone wants to get their hands on your device for malicious purposes — it's "who are they, and what could they do once they had it?" The first question is specific to your product; the second is answerable once you know how attackers actually approach hardware, which is what this talk works through.

**Six bins, roughly by cost and invasiveness**

1. **Research** — datasheets, third-party teardowns, extracted firmware, even social engineering against support staff. The goal isn't just "how does this work" but "where did the designers make an assumption they never actually enforced" — every attack downstream starts by invalidating one of those.
2. **Passive observation and logical attacks** — probing exposed ports and internal signals, checking whether the debug port is locked, brute-forcing a short password, replaying a captured transaction, or just fuzzing the UART with garbage. The 2010 PlayStation 3 hack started here: watching signals to the console's memory revealed a race condition that led to full compromise.
3. **Physical modification** — cutting a trace, swapping a strap resistor to change what hardware revision the firmware thinks it's running on, injecting a false signal onto an analog sensor line, or pushing the device outside its rated environmental range to see what breaks.
4. **Side-channel attacks** — extracting secrets from what a device leaks just by operating, without any modification at all. Timing is the easiest to grasp: a naive `strcmp`-style password check returns faster on the first mismatched byte, which turns a billion-guess brute force into 36 guesses per digit (a real, shipped "secure" external hard drive was broken exactly this way through its error LED). Power analysis goes further — simple power analysis can read key bits directly off a single trace for algorithms like textbook RSA, and differential power analysis uses difference-of-means statistics across thousands of traces to recover an AES key one byte at a time, without ever attacking AES itself.
5. **Fault injection** — deliberately pushing a device outside its operating envelope to induce a skipped instruction, a corrupted fetch, or a flipped memory value: a crowbar glitch on the supply rail, clock double-pulsing, EM pulses, or a laser on a decapped die. This is exactly how the Xbox 360 was broken in 2011 — the second-stage bootloader's kernel hash check was a single conditional, and glitching past that one branch let attackers load an unsigned kernel.
6. **IC decapping and FIB editing** — for a sufficiently determined, resourced attacker, exposing the silicon opens up optical side-channels, laser fault injection, and literal circuit edits with a focused ion beam. Most devices don't need to defend against this tier — and part of good security engineering is deciding, deliberately, that they don't.

**The takeaway**

None of these attacks require a state-sponsored budget, and none of them are hypothetical — every technique in this talk has a real production device it's been used against. The point isn't to induce despair; it's to work backward from "what am I actually protecting, from whom, and via which of these six avenues" and spend defensive effort accordingly. Sometimes that's as simple as locking a debug port. Sometimes it's a lot more.

**Additional Resources**

- [Nothing is Safe (JawnCon 0x2)]({% post_url 2025-10-10-jawncon26-nothing-is-safe %}) — the same attack spectrum talk, with a full recording and a live DPA/fault injection demo on a ChipWhisperer Nano
- [All Your Bytes are Belong to Us]({% post_url 2025-12-01-all-your-bytes-are-belong-to-us %}) — the written companion on DigiKey/Maker.io, covering the same six levels in more depth
- [How Hardware Gets Hacked →](https://www.digikey.com/en/maker/search-results?t=Nathan%20Jones%20How%20Hardware%20Gets%20Hacked&f=1981359301) — a multi-part series walking through a complete attack and defense, from start to finish

[Session page →](https://www.crowdsupply.com/teardown/portland-2026/long-talk/nothing-is-safe-an-introduction-to-hardware-in-security)
