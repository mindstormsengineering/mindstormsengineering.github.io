---
layout: post
title: "Simulating Your Embedded Project on Your Computer (Part 1)"
date: 2024-10-02
type: article
subjects:
  - firmware
  - education
excerpt: >
  The case for simulating your embedded project on a desktop machine — and how
  to do it with the simplest possible approach: swapping hardware I/O for
  printf and scanf, with practical details on making it non-blocking and readable.
---

*Originally published on [EmbeddedRelated](https://www.embeddedrelated.com/showarticle/1695.php).*

![Embedded project simulation on desktop]({{ '/assets/simulating_p1/simulation.png' | relative_url }})

Embedded developers are tied to their hardware in ways that software developers are not: you cannot easily run your code without the board, the sensors, or the physical setup. This first article in a two-part series makes the case that simulation — running your embedded application on a desktop machine — is worth the setup cost, and then shows the simplest possible way to do it. The prerequisite is "isolating the madness": structuring your code so that hardware-dependent operations are encapsulated behind an interface that can be swapped at compile time. With that in place, the simplest simulator replaces every output with `printf` and every input with `scanf`, producing a command-line interface that works immediately on any machine with a C compiler.

The article works through the practical details that trip people up: how to make `scanf` non-blocking so it does not halt the simulation while waiting for input, how to use ANSI escape codes to make terminal output more readable, and what kinds of bugs this approach is and is not suited to catching. A companion GitHub repo provides working implementations of every technique demonstrated.

Part 1 is explicitly for engineers who want a quick win — a simulator running in an afternoon — rather than a production-grade virtual environment. Part 2 picks up with two more capable options: full virtual hardware simulators (Wokwi, Renode, QEMU, Proteus) that mimic the MCU itself, and a PyQt GUI as a richer front end.

[Read the full article →](https://www.embeddedrelated.com/showarticle/1695.php)
