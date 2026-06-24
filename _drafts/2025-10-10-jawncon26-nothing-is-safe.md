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

Every electronic device that someone can physically touch is susceptible to hardware attacks — credit cards, key fobs, smart meters, industrial controllers — regardless of whether it has a network radio. The talk surveys the landscape of hardware attack techniques, organized roughly by cost, skill, and invasiveness. The goal isn't to induce panic but to give embedded engineers a clear picture of what the threat space actually looks like so they can make intentional decisions about where to spend defensive effort.

**The attack spectrum**

1. **Reconnaissance** — reading datasheets, finding community teardowns, reviewing PCB photos from FCC filings. Costs nothing, requires no hardware, and routinely reveals chip identities, debug port locations, and update mechanisms before an attacker ever touches the device.

2. **Snooping exposed interfaces** — attaching a logic analyzer or UART adapter to accessible debug headers. JTAG, SWD, UART, and I2C ports left enabled on production devices are a direct path to firmware extraction or live debugging. A $20 tool is sufficient.

3. **PCB modification** — cutting traces, rerouting signals, replacing components. Requires a soldering iron and some patience, but nothing exotic. Common targets include bypass capacitors near voltage regulators (relevant to fault injection) and pull-up/pull-down resistors that control boot mode selection.

4. **Side-channel attacks** — extracting secrets from timing, power consumption, or electromagnetic emissions without physically modifying the device. The talk demonstrates a differential power analysis (DPA) attack on AES using the ChipWhisperer Nano: capture a few thousand power traces during encryption, partition them by a bit of a hypothesized key byte, average each partition and subtract — a correlation spike appears at the moment the correct key hypothesis matches the actual intermediate computation. Repeat for each of the 256 key byte candidates and all 16 bytes of the key.

5. **Fault injection** — forcing computational errors by briefly glitching the supply voltage or using an electromagnetic pulse to cause a targeted instruction to fail or be skipped. The talk shows how a well-timed voltage glitch can cause a password comparison to pass without knowing the password.

6. **IC decapping and FIB editing** — chemically or mechanically removing the chip package to expose the die, then using a focused ion beam to cut or deposit conductors. This requires a well-equipped lab and significant expense, but it has been used against production silicon to recover keys and bypass security fuses.

**Countermeasures**

Countermeasures exist at every level. Random delays and constant-time comparison functions blunt timing attacks. Locking JTAG and disabling UART before shipping costs nothing. Glitch detectors and brownout circuits can abort sensitive operations under anomalous supply conditions. The right question to ask isn't "can my device be attacked" (it can) but "what is a realistic attacker's capability, and am I making it harder than it's worth?"

The talk closed with a Kahoot! — the prize was a ChipWhisperer Nano and a copy of *The Hardware Hacking Handbook*, so there was genuine motivation to pay attention.

The written companion to this talk is ["All Your Bytes are Belong to Us"](https://www.digikey.com/en/maker/blogs/2025/all-your-bytes-are-belong-to-us), a survey article I wrote for DigiKey's Maker.io that covers the same attack spectrum with more detail on each level.

[Session page →](https://jawncon.org/schedule0x2.html#4)
