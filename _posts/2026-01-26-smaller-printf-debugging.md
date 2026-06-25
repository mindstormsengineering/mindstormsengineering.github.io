---
layout: post
title: "Smaller printf Debugging"
date: 2026-01-26
type: article
subjects:
  - firmware
  - debugging
venue: DigiKey
excerpt: >
  Printf adds over 4 kB of flash just for a single call. This article benchmarks
  a range of techniques for shrinking that footprint, from compiler flags already
  on by default to swapping in a 200-byte binary serialization library.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/tutorials/2026/smaller-printf-debugging).*

![Message rate versus flash size for various printf implementations]({{ '/assets/smaller_printf/Smaller_26_speed-vs-size.png' | relative_url }})

On a microcontroller with 32 kB of flash, a single `printf` call costs 4.23 kB — over 13% of total flash. The article first surveys what's already working in your favor by default (newlib-nano instead of the full C library, `-Wl,--gc-sections` to discard unused code, the STM32 LL library over the HAL, no floating-point support in printf), then benchmarks explicit alternatives.

Switching from `printf` to `snprintf` with a custom output function cuts the footprint to about 3 kB. Substituting mpaland's lightweight snprintf implementation gets to around 2 kB. FlatBuffers drops it to about 1 kB. Bitproto, or a hand-rolled minimal serializer, can get debug messaging overhead under 200 bytes. Segger RTT is an honorable mention: not smaller than other options, but heap-free and with only about 1.3 kB of RAM overhead.

The tradeoff is speed: the speed-versus-size chart makes it visible that smaller implementations generally send fewer messages per second — bitproto being the notable exception at both the smallest and fastest end.

[Read the full article →](https://www.digikey.com/en/maker/tutorials/2026/smaller-printf-debugging)
