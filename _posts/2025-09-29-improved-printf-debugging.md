---
layout: post
title: "Improved printf Debugging"
date: 2025-09-29
type: article
subjects:
  - firmware
  - debugging
venue: DigiKey
excerpt: >
  Two additions that make printf debugging significantly more useful: automatic
  source location tagging via C macros, and severity-level filtering with
  compile-time removal of the entire debug subsystem.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/tutorials/2025/improved-printf-debugging).*

![Adding severity levels to debug output]({{ '/assets/improved_printf/Improved_02_Adding-severities.png' | relative_url }})

A bare `printf("here\n")` tells you almost nothing once your codebase has more than a handful of print statements. Two additions change that substantially. The first wraps `printf` in a macro that automatically prepends the file, line number, and function name using `__FILE__`, `__LINE__`, and `__func__` — turning every message into something immediately locatable and searchable without manual annotation.

The second adds severity levels (INFO, WARNING, ERROR) and a global logging threshold, so you can dial back output to just warnings and errors in the field while keeping verbose info logs available during development. A compile-time `#if DEBUG` guard lets the assembler emit zero debug code in production builds.

Both additions together fit in about 20 lines of C.

[Read the full article →](https://www.digikey.com/en/maker/tutorials/2025/improved-printf-debugging)
