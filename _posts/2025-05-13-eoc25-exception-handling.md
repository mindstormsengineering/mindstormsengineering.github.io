---
layout: post
title: "Exception Handling (EOC 2025)"
date: 2025-05-13
type: tutorial
subjects:
  - firmware
  - architecture
venue: Embedded Online Conference
excerpt: >
  Workshop slides and recording from the Embedded Online Conference 2025, covering
  how to cleanly and simply detect, propagate, and handle exceptions in embedded C/C++.
documents:
  - title: "Slides (PDF)"
    url: /assets/eoc25_exception_handling/Exception_Handling.pdf
    type: pdf
---

*Workshop given at the [Embedded Online Conference](https://embeddedonlineconference.com/session/Exception_Handling), May 2025.*

{% include youtube.html id="D8QEJk2Grbg" %}

The workshop opens with a distinction that shapes everything that follows: *errors* and *exceptions* are not the same thing. Errors are bugs — dereferencing a null pointer, calling a function before initializing the peripheral it depends on, taking the square root of a negative number. They represent things that shouldn't happen, and when they do the right response is usually a reset or a safe-mode transition, not a recovery attempt. Exceptions are different: I2C timeouts, out-of-range sensor readings, checksum failures on received data. They represent things that *can legitimately occur* during normal operation and that a well-designed system should handle gracefully. Conflating the two leads to either over-engineering (defensive code for scenarios that indicate a bug) or under-engineering (silently swallowing failures that should propagate).

**Identifying exceptions**

The workshop is structured as hands-on exercises around an Arduino test harness with temperature sensors and accelerometers (in Wokwi). We start at leaf functions — the I2C read, the ADC conversion, the buffer write — because that's where something can first go wrong. Working through the test harness, we annotate each leaf function with the exceptions it can detect: conversion timeouts, values outside a physical plausible range, communication errors.

**Reporting exceptions**

Once a leaf function detects an exception, it needs to communicate that to its caller. We cover six mechanisms in embedded context: try/catch, return values (with C++23's `[[nodiscard]]` attribute to prevent callers from silently ignoring the result), output parameters, local variables (i.e. `errno`, and signals/callbacks. Each has trade-offs in verbosity, expressiveness, and compatibility with coding standards — the workshop walks through examples of each and discusses when each makes sense.

**Responding to exceptions**

Not every caller is the right place to handle every exception. The question is which layer in the system has the context to make a meaningful decision — whether to retry, degrade gracefully, surface an error to the user, or escalate to a system-level reset. We work through examples of propagating exceptions up the call stack without losing information, and discuss how to design interfaces that make the exception path as clear as the happy path.

[Session page →](https://embeddedonlineconference.com/session/Exception_Handling)
