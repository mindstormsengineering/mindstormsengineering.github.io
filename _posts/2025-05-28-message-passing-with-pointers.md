---
layout: post
title: "Message Passing with Pointers"
date: 2025-05-28
type: article
subjects:
  - firmware
  - education
excerpt: >
  Why passing large structs by pointer instead of by value saves memory copies
  and instruction cycles in RTOS task communication — and the three ownership
  patterns that make it safe to do so.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/tutorials/2025/message-passing-with-pointers).*

![Three patterns for passing pointers between RTOS tasks]({{ '/assets/message_passing_with_pointers/three_ways.png' | relative_url }})

In an RTOS application with multiple tasks passing large structs between them, passing by value can mean copying the same data five separate times. Passing a pointer instead reduces that to one copy — and benchmarking on Compiler Explorer shows roughly 25% fewer lines of generated code for a struct containing a 16-element integer array, with further gains as the data gets larger.

The tricky part is ownership. Three patterns cover the main cases: the sender allocates memory and posts a pointer, the sender allocates memory and the receiver pulls a pointer when ready, or the receiver pre-allocates and the sender fills it in. Each avoids the redundant copies, but each requires the system designer to be explicit about which task owns the data at any given moment — and to guard against the four hazards of pointer-passing: NULL dereference, memory leaks, race conditions, and dangling pointers.

The patterns have different strengths depending on task topology. All three work cleanly in a one-sender, one-receiver pipeline; complications arise with multiple senders, multiple receivers, or when tasks are chained and each hands the data to the next.

[Read the full article →](https://www.digikey.com/en/maker/tutorials/2025/message-passing-with-pointers)
