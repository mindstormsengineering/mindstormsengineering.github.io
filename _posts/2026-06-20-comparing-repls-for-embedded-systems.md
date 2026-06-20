---
layout: post
title: "Comparing REPLs for Embedded Systems"
date: 2026-06-20
published: false
type: article
subjects:
  - firmware
  - education
excerpt: >
  MicroPython, the Zephyr shell, Lua, and Forth, evaluated for embedded
  development on ease of onboarding, compiled size, C/C++ interoperability,
  and overall fit.
---

*Not yet published. Update this section and add a CTA link when the article goes live.*

![]({{ '/assets/comparing_repls/cover.png' | relative_url }})

An interactive serial REPL makes it easy to prototype on an embedded system, inspect state, and modify configuration without a debugger. Four tools cover most of this space: MicroPython, the Zephyr shell, Lua, and Forth. The article evaluates each on three axes: how hard it is to reach a prompt on both supported and brand-new hardware, how large the compiled footprint is, and how difficult it is to interface with existing C/C++ code.

MicroPython is the most capable — full Python language, extensive libraries — but also the largest at 277 kB and 50–250× slower than C, and porting to a new MCU is significant work. The Zephyr shell is the smallest (44 kB), fastest, and easiest to interface with C/C++, but it isn't an interpreted language, so you can't write loops or declare variables at the prompt. Lua (144 kB, 10–50× slower than C) is mature, portable, and hits a compelling middle ground between capability and size. Forth is the smallest interpreted option at 25 kB with speeds competitive with Lua, but its stack-based RPN syntax is unfamiliar to most developers.

The article's recommendation is Lua for most use cases: capable enough for real scripting, small enough for constrained devices, and portable enough that porting effort amortizes well across multiple targets.
