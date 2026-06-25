---
layout: post
title: "The Power of a Look-up Table (EOC 2024)"
date: 2024-05-02
type: talk
subjects:
  - firmware
  - architecture
venue: Embedded Online Conference
excerpt: >
  Slides from the Embedded Online Conference 2024: what happens when you think of
  an array as a fixed-size O(1)-access structure rather than just a collection of
  values — and how that unlocks fast math, state machines, jump tables, DDS, and
  more.
documents:
  - title: "Slides (PDF)"
    url: /assets/eoc24_power_of_a_lut/The_Power_of_a_Look_up_Table.pdf
    type: pdf
---

*Talk given at the [Embedded Online Conference 2024](https://embeddedonlineconference.com/session/The_Power_of_a_Look_up_Table), May 2024.*

{% include youtube.html id="JfO25B_9zwk" %}

Most embedded developers have used a look-up table for fast trig or sine wave generation. Fewer have thought about why that works, and fewer still have followed that reasoning to its natural conclusion. That's what this talk was about.

The key reframe: stop thinking of an array as "a collection of values" and start thinking of it as "a fixed-size structure with O(1) access via an integer index." That's a subtle shift, but it changes what you see when you look at a problem.

**What the reframe unlocks**

Once you think in terms of O(1) indexed access, a lot of problems start looking like look-up table problems:

- **Fast math** — precompute expensive transcendental functions (sine, cosine, square root, logarithm) at compile time or startup. At runtime, an index and a memory access replaces floating-point computation.

- **Table-based initialization** — instead of a long sequence of `peripheral_init()` calls, store configuration structs in an array and loop over it. The initializer loop becomes trivial; the interesting content is declarative data.

- **Simple polymorphism** — an array of function pointers, indexed by a type tag or enum, dispatches to different implementations without a switch statement. It's a lightweight vtable.

- **Simplifying complex conditionals** — nested if-else trees that map inputs to outputs are often better expressed as an array indexed by input. The structure of the logic becomes visible in the data rather than buried in branching code.

- **Jump tables and state tables** — the classic FSM implementation: a 2D array indexed by current state and input event, containing either next states or transition functions. The state machine logic lives in the data.

- **Simulating digital hardware** — truth tables, encoder/decoder logic, combinational circuits. If the input is small enough to enumerate, the output is just a table lookup.

- **Direct digital synthesis (DDS)** — precompute a waveform, accumulate a phase increment, and index into the table. Arbitrary waveform generation at a fraction of the compute cost of real-time synthesis.

- **Capturing program logic as data** — the general principle behind all of the above: when the "logic" of your program can be expressed as a mapping from input to output, consider whether that mapping belongs in code or in a table.

**The mind-bending demo**

I closed the talk with what I still think is the most interesting example: a complete CLI parser implemented in about 60–70 lines of C. The parser uses a tree to represent the command hierarchy — each node can have sub-commands — and an array within each node to hold the possible inputs at that level. Adding a new command means adding an entry to an array. The dispatch logic doesn't change. The parser is small because almost all of its "intelligence" lives in the data, not the code.

The deeper point is that this generalizes. If you think carefully about what data structure the problem *actually* has the shape of — array, tree, stack, linked list — you often find that representing the problem in that structure and then operating on it produces dramatically simpler, more powerful code than expressing the same logic as procedural control flow.

[Session page →](https://embeddedonlineconference.com/session/The_Power_of_a_Look_up_Table)
