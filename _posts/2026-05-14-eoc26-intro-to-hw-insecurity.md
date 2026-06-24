---
layout: post
title: "Introduction to Hardware (In)Security with the ChipWhisperer-Nano (EOC 2026)"
date: 2026-05-14
type: tutorial
subjects:
  - security
  - hardware
  - education
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

This was one of my favorite things I've gotten to do: bring a hands-on hardware security workshop to an online audience. Jacob was kind enough to mention he'd taken an earlier version of this workshop in person, which both flattered me and raised the stakes considerably.

The workshop had three parts: context on the hardware attack sequence, a deep dive into side-channel attacks (specifically differential power analysis), and a demonstration of fault injection. The ChipWhisperer Nano was the star — if you had one, you could follow along live. If not, I provided pre-collected datasets so you could still run the exercises.

**The hardware attack sequence**

I opened by situating DPA and fault injection within the broader attack sequence I usually teach. These aren't the first tools an attacker reaches for. Before getting to side channels, they've probably done reconnaissance, probed exposed interfaces, and attempted simpler things. Understanding this helps engineers think about where to spend their defensive effort.

**Side-channel attacks and DPA**

The core of the workshop was a differential power analysis attack on AES. The setup: a target microcontroller running AES encryption, and the ChipWhisperer Nano measuring its power supply while it works. The goal is to extract the secret key without ever reading it directly.

The key insight behind DPA is that cryptographic operations aren't informationally isolated — the power the chip consumes is correlated with the data it's processing. Specifically, we used the Hamming weight model: more transistors switching means more power consumed, and that correlates with the number of set bits in intermediate values.

The attack worked like this:
1. Send the target many known plaintexts and collect a power trace for each.
2. Make a guess about one byte of the key.
3. Using that guess and the known inputs, compute the predicted output of the AES S-box for each trace.
4. Group the traces by whether the least significant bit of the predicted S-box output was 0 or 1.
5. Average the two groups and subtract. If your key guess was right, you'll see a spike at the moment the S-box computation occurred. If it was wrong, you'll see noise.
6. Repeat for all 256 possible values of that key byte, find the guess that produces the highest peak, and you've recovered a byte of the key. Then repeat for all 16 bytes.

We implemented this in Jupyter notebooks — participants worked through exercises building up from plotting individual traces to performing the full attack. Watching attendees get that first peak and realize they'd just broken AES on a live device was genuinely satisfying.

**Fault injection**

Time permitting, I also demonstrated a voltage glitching attack to bypass a password check. The target firmware does something like: compare input, branch if match, grant access. With a well-timed glitch on the supply voltage — brief enough to induce a fault without crashing the device — you can skip the branch instruction and get access without knowing the password. The ChipWhisperer Nano has hardware support for triggering these glitches with nanosecond precision.

**The takeaway**

The message I always close with: these attacks exist, and for many devices they're not exotic. The response isn't panic — it's intentionality. Security has to be a design criterion from the start, not a retrofit. Analyze who might want access to your device and what they're capable of. Lock debug ports on production devices. Use constant-time comparisons. Consider whether your update mechanism leaks firmware in plaintext. Most of the low-hanging countermeasures are free.

I'm happy to answer questions from anyone who got stuck on the exercises or wants to go deeper. Find me on LinkedIn or by email.

For a deeper written treatment of the DPA technique, ["Breaking AES with an Oscilloscope"](https://www.embeddedrelated.com/showarticle/1761.php) on EmbeddedRelated covers the same attack with more detail on the math and practical countermeasures.

[Session page →](https://embeddedonlineconference.com/session/introduction_to_hardware_in_security_with_the_chip_whisperer_nano)
