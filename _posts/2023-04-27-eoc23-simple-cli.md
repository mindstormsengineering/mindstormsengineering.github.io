---
layout: post
title: "Building a Simple Command-Line Interface (EOC 2023)"
date: 2023-04-27
type: talk
subjects:
  - firmware
  - tooling
  - education
excerpt: >
  Slides from the Embedded Online Conference 2023: how to add a lightweight
  command-line interface to an embedded system over UART, from parsing input to
  dispatching commands and handling arguments.
documents:
  - title: "Slides (PDF)"
    url: /assets/eoc23_simple_cli/Building_a_Simple_Command_Line_Interface.pdf
    type: pdf
---

*Talk given at the [Embedded Online Conference 2023](https://embeddedonlineconference.com/session/Building_a_Simple_Command_Line_Interface), April 2023.*

A command-line interface over UART is one of the most useful things you can add to an embedded system and one of the least talked-about. It turns a device that communicates entirely through LEDs and log output into something you can actually interrogate: ask it its current state, change a parameter, trigger a test routine. It's indispensable during development and surprisingly useful in production.

**Why a CLI belongs in your firmware**

The case for a CLI is mostly about development speed. Instead of reflashing to change a parameter, you change it over serial. Instead of adding debug printf statements to see some state, you add a command that prints it on demand. Instead of guessing whether a peripheral is working, you write a command that exercises it directly. The overhead is small; the payoff is large.

**Parsing UART input**

The first step is getting text into the system. I walked through reading characters from UART, accumulating them into a line buffer, and detecting line termination. This is straightforward in principle but has a few practical details: handling backspace, avoiding buffer overflows, and not blocking the rest of the firmware while waiting for input.

**Command dispatch**

Once you have a complete line, you need to match it to a command. I covered a table-based dispatch approach: a struct containing a command name string and a function pointer, with a table of those structs that the CLI searches linearly. For small command sets this is fast enough and dead simple. Each command handler receives the remainder of the input line and can parse its own arguments.

**Handling arguments**

Commands with parameters need argument parsing. I showed a simple tokenization approach — splitting the input on whitespace and passing the resulting tokens to the handler — alongside conversion utilities for integers and floating-point values. Keeping argument parsing in the handler rather than in the dispatch layer means each command can define exactly what it expects without a central parser that needs to know every command's argument types.

The full implementation is on GitHub as `simple-cli`, with examples for both STM32 and Arduino.

**Additional Resources**

- [Building a Simple Command-Line Interface (Teardown 2024)]({% post_url 2024-06-21-teardown24-simple-cli %}) — the same talk given at Teardown Portland 2024, with a recording
- [simple-cli on GitHub →](https://github.com/nathancharlesjones/simple-cli)

[Session page →](https://embeddedonlineconference.com/session/Building_a_Simple_Command_Line_Interface)
