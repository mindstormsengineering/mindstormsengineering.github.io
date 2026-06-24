---
layout: post
title: "Retro Computing with the Hackaday Supercon Badge 'Voja4' (Teardown 2024)"
date: 2024-06-22
type: tutorial
subjects:
  - hardware
  - architecture
  - education
excerpt: >
  Workshop slides from Teardown Portland 2024: an introduction to the Voja4 retro
  computer badge, its 4-bit architecture and instruction set, and hands-on assembly
  programming.
documents:
  - title: "Slides (PDF)"
    url: /assets/teardown24_voja4/teardown-2024-nathan-jones-voja4.pdf
    type: pdf
---

*Workshop given at [Teardown Portland 2024](https://www.crowdsupply.com/teardown/portland-2024/workshop/retro-computing-with-the-hackaday-supercon-badge-voja4), June 2024.*

The Voja4 is the Hackaday Supercon 2022 badge: a hand-assembled retro computer with a custom 4-bit CPU, a twelve-button/LED front panel, and an instruction set small enough to hold in your head. I brought it to Teardown to run a hands-on workshop, and it turned out to be a great venue for it — Teardown draws hardware people who appreciate the gap between "interesting architecture" and "I've actually programmed the thing."

**Architecture and ISA overview**

We started with the architecture. The Voja4 emulates a 4-bit custom CPU on a PIC24 microcontroller. The instruction set is compact: 32 opcodes, 12-bit instruction words, where four bits encode the opcode and two four-bit fields carry operands or immediates. The front panel maps directly to the instruction format — programming in binary isn't a novelty here, it's the natural interface for the machine.

I walked through the ISA in enough detail that participants could read and write simple programs without constantly consulting an opcode table. The instruction set is small enough that this is achievable in under an hour, which is part of what makes the Voja4 a genuinely good teaching tool for processor architecture.

**Loading an example and getting to running code**

Rather than starting from a blank program, participants loaded a pre-written example over UART — the badge has a serial interface that makes this straightforward. Getting to running code quickly matters in a hands-on session: it means everyone has a starting point that works, and the interesting part (modifying it, breaking it, fixing it) can begin right away.

**Writing your own programs and debugging**

From there, participants had time to write their own programs. I covered two things that make this considerably less painful: debugging strategies on the badge itself, and using flowcharts as a planning tool before writing Voja4 assembly.

Debugging on the Voja4 is a manual process — there's no debugger in the modern sense, so you're reasoning from outputs and intermediate register states. That constraint is actually a feature for a teaching context; it builds exactly the kind of careful, step-by-step mental model of execution that tends to get fuzzy when a breakpoint is always available.

The flowchart technique is something I use for any assembly-level programming: sketch the control flow in plain terms before writing a single instruction. With a constrained instruction set like the Voja4's, the translation from flowchart to code is nearly mechanical once you're familiar with the opcodes.

- [Badge tools and software (GitHub) →](https://github.com/Hack-a-Day/2022-Supercon6-Badge-Tools)
- [Voja4 badge on Tindie →](https://www.tindie.com/products/0xc0decafe/supercon-2022-badge-voja4/)
