---
layout: post
title: "Comparing MicroPython, Zephyr, Lua, and Forth"
date: 2026-07-13
type: article
subjects:
  - firmware
  - tooling
venue: DigiKey
excerpt: >
  MicroPython, the Zephyr shell, Lua, and Forth, evaluated head-to-head on an
  STM32 Nucleo board for time to a working REPL, compiled footprint, execution
  speed, and how hard each is to interface with existing C/C++ code.
documents:
  - title: "Comparing MicroPython, Zephyr, Lua, and Forth (PDF)"
    url: /assets/comparing_lua/comparing_repls.pdf
    type: pdf
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/blogs/2026/comparing-micropython-zephyr-lua-and-forth).*

![Comparison table scoring MicroPython, Zephyr, Lua, and Forth (red/yellow/green) across getting started, C/C++ integration, code size, execution speed, and features]({{ '/assets/comparing_lua/summary_table.png' | relative_url }})

An interactive serial REPL is one of the fastest ways to prototype on an embedded system, inspect state, or tweak configuration without a debugger. The article puts four options for reaching one head-to-head on an STM32 Nucleo-F411: MicroPython, the Zephyr shell utility, Lua, and Forth — scored on how fast each reaches a working prompt (on supported hardware and on a brand-new device), how large the compiled binary is, how much slower than native C/C++ it runs, and how hard it is to call into (or be called from) existing C/C++ code.

MicroPython wins on capability — the full Python language plus its library ecosystem — but it's also the heaviest: 277 kB compiled, 50–250x slower than native code, and porting it to an unsupported MCU can run from a few days to two months. The Zephyr shell sits at the opposite extreme: 44 kB, the fastest of the four since application code is just C, and trivial to interface with existing C/C++ — but it isn't an interpreted language, so there's no REPL in the "declare a variable and write a loop" sense. Lua (144 kB, 10–50x slower than native) lands in the middle: mature, genuinely interpreted, easy to embed, and consistently cheaper to port to a new MCU than either MicroPython or Zephyr. Forth is the outlier: only 25 kB and the smallest interpreted option by far, but its stack-based RPN syntax gets unwieldy fast once you're juggling more than a couple of variables.

The article's recommendation is Lua for most projects: capable enough for real prototyping, small enough for constrained devices, and — critically for anyone targeting more than one MCU — the one option where porting effort stays predictable instead of ballooning with each new device tier.

[Read the full article →](https://www.digikey.com/en/maker/blogs/2026/comparing-micropython-zephyr-lua-and-forth)
