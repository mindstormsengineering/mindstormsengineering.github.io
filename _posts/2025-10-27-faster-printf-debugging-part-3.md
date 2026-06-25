---
layout: post
title: "Faster printf Debugging (Part 3)"
date: 2025-10-27
type: article
subjects:
  - firmware
  - debugging
venue: DigiKey
excerpt: >
  Part 3 replaces human-readable text with binary serialization, reaching
  38.9k–117.8k messages per second using MessagePack, FlatBuffers, and bitproto
  — a 274–829× improvement over the original baseline.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/tutorials/2025/faster-printf-debugging-part-3).*

![Full summary chart of all printf speed optimizations across all three articles]({{ '/assets/faster_printf_p3/summary.png' | relative_url }})

The bottleneck at the end of Part 2 was no longer the UART or the processor — it was the text formatting. A "Value of counter: %03d\n" message is 22 characters; a binary-serialized equivalent can fit in 7 bytes. Part 3 benchmarks three serialization libraries over a buffered USB connection: MessagePack (38.9k msg/sec, 26.9 kB flash), FlatBuffers (~36k msg/sec at 75.9% CPU utilization, 18.1 kB flash), and bitproto (117.8k msg/sec, 16.6 kB flash). A hand-rolled minimal sprintf lands at 14.2k msg/sec with just 4.3 kB of flash.

The full three-article summary chart puts it all in context: 142 msg/sec at the original baseline versus up to 117.8k msg/sec with bitproto. The primary tradeoff at the binary serialization tier is portability and human readability — you'll need a deserializer on the host and your logs won't be grep-friendly.

[Read the full article →](https://www.digikey.com/en/maker/tutorials/2025/faster-printf-debugging-part-3)
