---
layout: post
title: "You Don't Need an RTOS (Part 2)"
date: 2024-05-07
type: article
subjects:
  - firmware
  - education
excerpt: >
  Three targeted improvements to the basic superloop — task priorities,
  interrupt-driven tasks, and finite state machines — that bring worst-case
  response time close to a preemptive RTOS while eliminating race conditions.
---

*Originally published on [EmbeddedRelated](https://www.embeddedrelated.com/showarticle/1652.php).*

![The Superduperloop with task priorities and FSMs]({{ '/assets/rtos_p2/superduperloop.png' | relative_url }})

Part 2 of the "You Don't Need an RTOS" series takes the simple superloop from Part 1 and applies three targeted modifications that together produce what I call the "Superduperloop": a non-preemptive scheduler whose worst-case response time approaches that of a preemptive RTOS. The three changes are adding task priorities (via if/else-if chains so higher-priority tasks preempt lower ones at loop boundaries), adding interrupt service routines for truly time-critical work, and restructuring tasks as finite state machines so long-running operations yield voluntarily without blocking the scheduler. Three different methods for assigning task priorities are discussed and demonstrated.

A concrete benchmark shows the Superduperloop besting a preemptive RTOS on worst-case response time in a specific task set, by exploiting the determinism of non-preemptive scheduling. The article also covers how to incorporate a sleep mode when there is no work to be done, and introduces the time-triggered scheduler as an alternative design for difficult task sets.

[Read the full article →](https://www.embeddedrelated.com/showarticle/1652.php)
