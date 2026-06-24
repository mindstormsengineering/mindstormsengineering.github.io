---
layout: post
title: "Nothing Is Safe: An Introduction to Hardware (In)Security (JawnCon 0x2)"
date: 2025-10-10
type: talk
subjects:
  - security
  - hardware
  - education
excerpt: >
  Slides and recording from JawnCon 0x2: a survey of hardware attack techniques
  organized as a spectrum from cheap and easy reconnaissance all the way to focused
  ion beam surgery on bare silicon.
documents:
  - title: "Slides (PDF)"
    url: /assets/jawncon26_nothing_is_safe/Nothing is Safe.pdf
    type: pdf
---

*Talk given at [JawnCon 0x2](https://jawncon.org/schedule0x2.html#4), October 2025.*

{% include youtube.html id="FZqHA2Kq8oc" %}

JawnCon was a blast. It's the kind of conference where people are genuinely excited to be there, and that energy is contagious. I got to talk about hardware security — one of my favorite topics — in front of an enthusiastic crowd, and I even ran a Kahoot! with a ChipWhisperer Nano and a couple copies of *The Hardware Hacking Handbook* as prizes. Not bad.

The core argument of the talk is right there in the title: nothing is safe. Every electronic device that someone can physically touch is susceptible to hardware attacks, regardless of whether it has a network radio. The credit cards in your wallet, your car key fob, your smart meter — none of them are immune. Understanding the landscape of attacks isn't about paranoia; it's about knowing what your device actually needs to defend against.

**The attack spectrum**

I organized the talk around a spectrum of attacks, roughly ordered by cost, skill, and invasiveness:

1. **Reconnaissance** — reading datasheets, finding teardowns online, reviewing PCB photos. Free, requires no hardware, and often yields more than you'd expect.

2. **Snooping** — attaching a logic analyzer to exposed UART, JTAG, or I2C interfaces. A $20 tool can read firmware update traffic or debug output that should have been disabled before shipping.

3. **PCB modification** — cutting traces, adding wires, swapping components. Takes some skill and a decent soldering iron, but nothing exotic.

4. **Side-channel attacks** — inferring secrets from timing, power consumption, or electromagnetic emissions. No physical modification required. I demonstrated a differential power analysis (DPA) attack on AES encryption using the ChipWhisperer Nano: collect a few thousand power traces, sort them by a bit of the encryption output, average and subtract — and a peak appears exactly where the key hypothesis is correct. It's elegant and deeply unsettling the first time you see it work.

5. **Fault injection** — inducing computational errors via voltage glitching or EMFI to skip instructions or corrupt comparisons. I showed how this can bypass a password check with a well-timed glitch on the supply rail.

6. **IC decapping and FIB editing** — removing the chip packaging, exposing the die, and using a focused ion beam to physically cut traces or deposit material. Expensive, requires a lab, but it's real and it's been used against production silicon.

**Countermeasures**

The point isn't hopelessness — it's intentionality. Countermeasures exist for every level. Random delays and constant-time comparisons defeat simple timing attacks. Non-default constants and control-flow verification resist fault injection. Locking the debug port before shipping costs almost nothing. The question is always: who might attack my device, and what's their realistic capability? Design accordingly.

The crowd had great energy and the Kahoot! generated some friendly competition. If you walked away with a ChipWhisperer Nano, I hope you're putting it to good use.

The written companion to this talk is ["All Your Bytes are Belong to Us"](https://www.digikey.com/en/maker/blogs/2025/all-your-bytes-are-belong-to-us), a survey article I wrote for DigiKey's Maker.io that covers the same attack spectrum with more detail on each level.

[Session page →](https://jawncon.org/schedule0x2.html#4)
