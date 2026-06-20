---
layout: post
title: "Thread-safe printf Debugging (Part 1)"
date: 2026-03-02
type: article
subjects:
  - firmware
  - education
excerpt: >
  Naive printf calls from ISRs or RTOS threads produce garbled output or worse.
  Part 1 works through three solutions — disabling interrupts, a mutex, and a
  double buffer — each better than the last but with its own caveats.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/tutorials/2026/thread-safe-printf-debugging-part-1).*

![Interrupt disable protecting a printf critical section]({{ '/assets/thread_safe_p1/disable_interrupts.png' | relative_url }})

Two RTOS threads calling `printf` at the same time will interleave their characters. Two ISRs doing the same can corrupt UART peripheral state. The naive fix — wrapping every printf in a critical section — works but blocks all other interrupts for as long as it takes to format and transmit the message, which at 3 Mbaud and 22 characters is still tens of microseconds.

Three progressively better approaches: disable interrupts around the entire call (simple, correct, blocks everything); use an RTOS mutex (correct for thread-to-thread communication, but mutexes can't be acquired from ISRs); use a double buffer that separates formatting from transmission so the critical section only covers the memory copy, not the UART write. The double buffer is the most capable solution but introduces its own race conditions — which Part 2 addresses.

[Read the full article →](https://www.digikey.com/en/maker/tutorials/2026/thread-safe-printf-debugging-part-1)
