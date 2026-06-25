---
layout: post
title: "You Don't Need an RTOS (Part 1)"
date: 2024-04-11
type: article
subjects:
  - firmware
  - architecture
venue: EmbeddedRelated
excerpt: >
  The case for the humble superloop as a serious scheduler — how to measure
  task deadlines and worst-case execution times, determine schedulability, and
  assign priorities before reaching for an RTOS.
---

*Originally published on [EmbeddedRelated](https://www.embeddedrelated.com/showarticle/1636.php).*

![Comparison of superloop and RTOS schedulers]({{ '/assets/rtos_p1/superloop_vs_rtos.png' | relative_url }})

"You don't need an RTOS" is a strong claim, but it is rooted in a real observation: most engineers who reach for a preemptive RTOS do so before doing the math to know whether they need one. An RTOS introduces the risk of race conditions — a class of failures that humans are particularly bad at reasoning about — and is only justified when a system's task set cannot be made schedulable without preemption.

This first article in a four-part series establishes the vocabulary needed to actually make that determination: deadlines, periods, worst-case execution times (WCET), and schedulability analysis. With those tools in hand, the argument is that a well-designed superloop can handle more task sets than engineers typically give it credit for — without the concurrency hazards an RTOS introduces. The article walks through how to measure WCET using a logic analyzer or serial converter, how to apply a utilization test to determine if a set of tasks is schedulable, and how to assign RTOS task priorities optimally when an RTOS is ultimately warranted.

By the end of Part 1, you will be able to calculate deadlines, periods, and WCETs for each task in your system, run a response-time analysis or utilization test to determine if the task set is schedulable with either architecture, and assign priorities optimally. It is the foundation for the three subsequent articles, which add priorities, interrupts, finite state machines, and a family of DIY inter-process communication mechanisms to the basic superloop.

**Additional Resources**

- [You Don't Need an RTOS (Teardown 2025)]({% post_url 2025-06-21-teardown25-you-dont-need-an-rtos %}) — a talk covering the schedulability analysis and the case for cooperative scheduling

[Read the full article →](https://www.embeddedrelated.com/showarticle/1636.php)
