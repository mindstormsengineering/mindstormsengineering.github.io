---
layout: post
title: "Introduction to Hardware (In)Security with the ChipWhisperer-Nano (EOC 2026)"
date: 2026-05-14
type: tutorial
subjects:
  - security
  - hardware
venue: Embedded Online Conference
excerpt: >
  Workshop slides, recording, and exercise files from the Embedded Online Conference 2026:
  hands-on differential power analysis and fault injection using the ChipWhisperer Nano.
documents:
  - title: "Slides (PDF)"
    url: /assets/eoc26_intro_to_hw_insecurity/intro_to_hw_insecurity.pdf
    type: pdf
  - title: "Exercise Files (ZIP)"
    url: /assets/eoc26_intro_to_hw_insecurity/eoc_files.zip
    type: zip
---

*Workshop given at the [Embedded Online Conference 2026](https://embeddedonlineconference.com/session/introduction_to_hardware_in_security_with_the_chip_whisperer_nano), May 2026.*

{% include youtube.html id="ldqvHjCgYu4" %}

A hands-on hardware security workshop built around the ChipWhisperer Nano, a development board designed specifically for learning side-channel analysis and fault injection. Participants who had one could follow along with live exercises; everyone else received pre-collected datasets so the analysis could still be run. The workshop focused predominantly on power side-channel attacks (split between understanding the technique and executing an actual DPA attack on AES) with the remaining time split between framing the attack landscape and a demonstration of fault injection.

**Context: where these attacks fit**

Side-channel and fault injection attacks are powerful, but they're not the first things an attacker tries. The workshop opens by situating DPA and glitching within the broader hardware attack sequence — reconnaissance, interface snooping, PCB modification — so participants understand what defensive measures matter most and at what point in the attack progression these techniques appear.

**Simple power analysis**

Before DPA, we spend time on simple power analysis (SPA): plotting individual power traces captured during AES encryption and observing that different operations consume measurably different amounts of power. The encryption rounds are visually distinct in the trace. This builds the intuition for *why* power consumption leaks information before we get into the statistics of extracting it.

**Differential power analysis on AES**

DPA exploits the relationship between a device's power consumption and the data it's processing. The specific model: the power a CMOS circuit consumes is proportional to the number of bits that switch state (the Hamming distance between successive values), which in turn correlates with the Hamming weight of intermediate computation results.

The attack on AES targets the output of the S-box substitution in the first round, since that value depends on only one byte of the key and the known plaintext. The procedure:

1. Encrypt many known plaintexts and capture a power trace for each (~2500 traces in the workshop exercises).
2. For each of the 256 possible values of a key byte, compute the predicted S-box output for each trace using that hypothesis and the known plaintext.
3. Partition the traces into two groups based on the least significant bit of the predicted S-box output.
4. Average each group and subtract. If the key hypothesis is correct, the traces are partitioned along a real physical boundary and the subtraction reveals a spike at the moment the S-box computation occurs. If the hypothesis is wrong, the partitioning is essentially random and the subtraction produces noise.
5. The hypothesis with the highest correlation peak is the correct key byte. Repeat for all 16 bytes.

The exercises build up to this incrementally: plotting traces, implementing the Hamming weight model, computing the difference of means, and finally iterating over all 256 hypotheses to recover a byte of the AES key.

**Fault injection**

The workshop closes with a demonstration of voltage glitching: briefly pulling down the supply voltage at a precisely timed moment to cause the target to execute an instruction incorrectly or skip it entirely. The specific example is bypassing a password comparison — a well-timed glitch on the supply rail causes any one of dozens of instructions to fail, granting access without knowing the password. The ChipWhisperer Nano has hardware support for triggering these glitches with nanosecond precision. This section works as a demonstration for everyone; running the hands-on exercises requires having the hardware.

For a deeper written treatment of the DPA technique, ["Breaking AES with an Oscilloscope"](https://www.embeddedrelated.com/showarticle/1761.php) on EmbeddedRelated covers the same attack with more detail on the math and practical countermeasures.

[Session page →](https://embeddedonlineconference.com/session/introduction_to_hardware_in_security_with_the_chip_whisperer_nano)
