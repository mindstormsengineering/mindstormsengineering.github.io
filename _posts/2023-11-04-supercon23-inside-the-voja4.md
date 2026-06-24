---
layout: post
title: "Inside the Voja4 (Hackaday Supercon 2023)"
date: 2023-11-04
type: talk
subjects:
  - hardware
  - architecture
  - education
excerpt: >
  Slides and recording from Hackaday Supercon 2023: an exploration of the elegant
  architecture behind the Voja4, the custom 4-bit retro computer badge designed by
  Voja Antonić.
documents:
  - title: "Slides (PDF)"
    url: /assets/supercon23_inside_the_voja4/Inside-the-Voja4.pdf
    type: pdf
---

*Talk given at [Hackaday Supercon 2023](https://hackaday.io/superconference/), November 2023.*

{% include youtube.html id="cUcKpRigZts" %}

The Supercon 2022 badge was the Voja4: a hand-assembled kit containing a custom 4-bit retrocomputer of Voja Antonić's design. If you've never seen one in person, the physical interface is unusual and instantly memorable — twelve buttons and twelve LEDs arranged on the front panel, corresponding directly to the 12-bit instruction format. You program it by entering binary. It looks like something out of an alternate 1970s.

For Supercon 2023, I gave a talk looking inside the architecture. I was happy to say yes.

**A custom ISA on a PIC24**

The Voja4 isn't a standalone CPU — it's a PIC24 microcontroller emulating a custom 4-bit processor in software. Voja designed the instruction set from scratch, and the choices he made are worth examining. The ISA supports 32 opcodes, derived from 12-bit instructions where four bits encode the opcode and two four-bit fields carry operands or immediate values.

The front panel isn't incidental to the design — it's load-bearing. The physical layout of the twelve switches and LEDs maps directly to the instruction word. You're not looking at a number; you're looking at the instruction itself, in binary, with your fingers on the bits. It's an unusually honest kind of human-machine interface.

**Is it Turing-complete?**

I spent some time on this question, which sounds academic but gets at something real: how much can you actually compute on a machine with 32 opcodes and constrained addressable memory? The instruction set doesn't include built-in multiplication, which sounds limiting until you work through how to implement it from shifts and adds. The more fundamental constraint is memory — the addressable space is small by design, and that's the practical ceiling more than the instruction set itself.

The theoretical answer is yes, with appropriate workarounds. I sketched a proposal for extending the addressable space through an external memory interface over serial, which would open up more ambitious programs without fundamentally changing the architecture.

**Why it's worth studying**

What I find most interesting about the Voja4 isn't the nostalgia angle — it's the clarity. Voja designed a processor that a human can hold in their head all at once: every opcode, every addressing mode, the full instruction encoding. That's a genuinely rare property, and it makes the Voja4 one of the best tools I know for building an intuition for how processors actually work at the architecture level, before the complexity of modern ISAs gets in the way.

The Hackaday writeup below has a good summary of the talk if you prefer reading to watching.

- [Supercon 2023: Exploring the Elegance of the Voja4 →](https://hackaday.com/2024/05/20/supercon-2023-exploring-the-elegance-of-the-voja4/)
- [Badge tools and software (GitHub) →](https://github.com/Hack-a-Day/2022-Supercon6-Badge-Tools)
- [Voja4 badge on Tindie →](https://www.tindie.com/products/0xc0decafe/supercon-2022-badge-voja4/)
