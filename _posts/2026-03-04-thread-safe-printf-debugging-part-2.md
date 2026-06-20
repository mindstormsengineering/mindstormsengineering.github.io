---
layout: post
title: "Thread-safe printf Debugging (Part 2)"
date: 2026-03-04
type: article
subjects:
  - firmware
  - education
excerpt: >
  Part 2 works through the race conditions in the double-buffer scheme from Part
  1, categorizes three types of critical sections, and applies three tools to
  protect them — then notes that even the C library itself may not be
  thread-safe.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/tutorials/2026/thread-safe-printf-debugging-part-2).*

![Garbled output caused by a thread-safety race condition]({{ '/assets/thread_safe_p2/threadSafe_02_garbled.png' | relative_url }})

The double buffer from Part 1 has three race conditions of its own. Part 2 works through each using a framework of three critical-section types: code that must be atomic (indivisible), code that can't run until after a specific event, and code that must run immediately before one. Each maps to one or more of three protective tools: global interrupt disable, a mutex, or C++ atomics — with the constraint that mutexes can't be released from ISRs.

Beyond the buffer itself, making the full logging path thread-safe also means ensuring that `snprintf` is re-entrant (which requires `<reent.h>` in most embedded C libraries), that `malloc` is protected if used, and that every other function in the call chain is thread-safe. The conclusion is that a properly thread-safe debug logger is a more involved undertaking than it first appears.

[Read the full article →](https://www.digikey.com/en/maker/tutorials/2026/thread-safe-printf-debugging-part-2)
