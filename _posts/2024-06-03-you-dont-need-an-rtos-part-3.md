---
layout: post
title: "You Don't Need an RTOS (Part 3)"
date: 2024-06-03
type: article
subjects:
  - firmware
  - architecture
venue: EmbeddedRelated
excerpt: >
  A survey of ready-to-use cooperative schedulers — Protothreads, ULWOS2,
  cocoOS, SST0/QV — alongside a walkthrough of how to implement thread flags,
  binary semaphores, and event flags on top of the Superduperloop from Part 2.
---

*Originally published on [EmbeddedRelated](https://www.embeddedrelated.com/showarticle/1653.php).*

![Cooperative scheduler options for embedded systems]({{ '/assets/rtos_p3/cooperative_schedulers.png' | relative_url }})

Part 3 addresses one of the main objections to the superloop: the RTOS primitives it lacks by default — semaphores, event flags, queues, and other inter-process communication (IPC) mechanisms that real systems depend on. Before adding these manually, the article surveys a set of off-the-shelf cooperative schedulers that already provide them: Protothreads, ULWOS2 (Ultra Light Weight OS 2), cocoOS, and SST0/QV from the QP Framework, each with a different set of OS primitives and licensing terms.

For engineers who want more control than these schedulers offer, the second half of the article demonstrates how to implement thread flags, binary semaphores, and event flags directly on top of the Superduperloop. The result is the "Superduperloop v2" — a non-preemptive scheduler with the IPC mechanisms most commonly needed in practice, written from scratch in a few dozen lines of C.

The article makes the case that adding IPC to the Superduperloop is not as hard as it might seem, and that doing so gives the engineer maximum control over timing behavior and system structure — something that off-the-shelf schedulers and RTOSes necessarily trade away for convenience. Part 4 completes the picture with mailboxes, queues, counting semaphores, the Observer pattern, and a dispatch queue.

**Additional Resources**

- [You Don't Need an RTOS (Teardown 2025)]({% post_url 2025-06-21-teardown25-you-dont-need-an-rtos %}) — a talk covering the schedulability analysis and the case for cooperative scheduling

[Read the full article →](https://www.embeddedrelated.com/showarticle/1653.php)
