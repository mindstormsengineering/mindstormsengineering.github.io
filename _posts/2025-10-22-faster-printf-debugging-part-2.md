---
layout: post
title: "Faster printf Debugging (Part 2)"
date: 2025-10-22
type: article
subjects:
  - firmware
  - debugging
venue: DigiKey
excerpt: >
  Part 2 pushes from 140 µs to 88 µs per debug message using asynchronous
  transmission and buffered USB — roughly 80× faster than the original baseline,
  though with significantly more implementation complexity.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/tutorials/2025/faster-printf-debugging-part-2).*

![Summary chart of printf timing optimizations through Part 2]({{ '/assets/faster_printf_p2/summary.png' | relative_url }})

Part 1 got the per-message time to 140 µs through hardware changes. Part 2 applies software techniques that are considerably harder to implement. Switching from blocking `printf` to `snprintf` with asynchronous DMA or interrupt-driven transmission frees the processor while bytes go out over the wire. Compiling at `-O3` reclaims a few more microseconds. Switching the transport from UART to USB CDC with a transmit buffer delivers the biggest remaining gain: 88 µs per message, with the processor only busy for about 63 µs of that.

The cumulative result across Parts 1 and 2 is approximately 80× faster than the original 7,030 µs baseline. The caveat: each technique here is meaningfully harder to implement than those in Part 1, and faster-for-its-own-sake is rarely justified — the right time to apply these is when you've confirmed that printf throughput is the actual bottleneck.

[Read the full article →](https://www.digikey.com/en/maker/tutorials/2025/faster-printf-debugging-part-2)
