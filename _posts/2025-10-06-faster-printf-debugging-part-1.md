---
layout: post
title: "Faster printf Debugging (Part 1)"
date: 2025-10-06
type: article
subjects:
  - firmware
  - education
excerpt: >
  Part 1 of a three-part series: hardware settings and one library swap reduce a
  22-character debug message from 7,030 µs to 140 µs on a Nucleo-F042K6 — a 50×
  speedup with three changes.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/tutorials/2025/faster-printf-debugging-part-1).*

![Summary chart of printf timing optimizations]({{ '/assets/faster_printf_p1/summary.png' | relative_url }})

Printf's speed problem is mostly a UART problem: at 38400 baud, transmitting even a short message takes milliseconds, which is long enough to disrupt timing-sensitive code or make printf too expensive to call often. Three changes address most of it without touching application code: run the processor at its full rated clock (8 → 48 MHz), raise the UART baud rate to the practical maximum (38400 → 3 Mbaud), and replace the STM32 HAL with the leaner LL driver for the UART peripheral. Together these take a 7,030 µs baseline to 140 µs — a 50× improvement.

The article also covers non-hardware approaches for cases where you want to call printf less even when it's fast: batching messages, simplifying format strings, shortening message text, and running your application in a host simulator where UART timing is irrelevant.

[Read the full article →](https://www.digikey.com/en/maker/tutorials/2025/faster-printf-debugging-part-1)
