---
layout: post
title: "Exception Handling (EOC 2025)"
date: 2025-05-13
type: tutorial
subjects:
  - firmware
  - education
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

I led this session as the opening workshop of EOC 2025, and I was genuinely excited — exception handling is one of those topics that embedded developers deal with constantly but rarely discuss in a structured way.

The first thing I wanted to nail down is the distinction between *errors* and *exceptions*, because I think conflating them leads to bad designs. Errors, to me, are bugs: dereferencing a pointer before allocating memory, taking the square root of a negative number — things that should never happen and indicate something has gone horribly wrong. The right response to a true error is usually a reset or a safe-mode fallback, not a recovery attempt. Exceptions are different: they're things that *might* legitimately occur during operation — an I2C timeout, a sensor value out of expected range, a checksum mismatch on received data — and that need to be handled gracefully.

The session was structured as a hands-on workshop. Attendees brought their own embedded projects (or used sample code I provided), and we worked through a progression together:

1. **Identifying exceptions at leaf functions** — where in your call stack are things that could go wrong? I2C reads, sensor polling, buffer writes. We instrumented those functions to detect and report exceptions back to the caller rather than silently failing or returning garbage.

2. **Propagating exceptions up the call stack** — once you detect something at the leaf level, how do you get that information to a layer that can actually do something about it? Return codes, output parameters, and C++ `std::expected` all came up here. I also mentioned `setjmp`/`longjmp`-inspired patterns for those deep in callback-heavy code, though I was careful to note that doesn't mean you should.

3. **Handling exceptions at the right level** — not every caller needs to respond to every exception. The question is which layer in the system actually has the context to make a meaningful decision.

One pattern that came up repeatedly — and that I enjoyed having a name for — is "car crash code" (sometimes called "brunge"): deeply nested if-else trees or chains of `goto cleanup` that make following the happy path feel like navigating a wreck. We looked at ways to restructure that code so exception paths are still readable without requiring heroics.

One audience member made a point I appreciated: the plain, verbose, check-the-error-code-at-every-step style has real merit, especially in MISRA-constrained embedded environments where `try`/`catch` is off the table. It's not elegant in the conventional sense, but it's regular, auditable, and meets a lot of coding standards. I think that's exactly right — the goal isn't cleverness, it's robustness with minimal effort.

[Session page →](https://embeddedonlineconference.com/session/Exception_Handling)
