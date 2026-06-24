---
layout: post
title: "You Don't Need an RTOS (Teardown 2025)"
date: 2025-06-21
type: talk
subjects:
  - firmware
  - architecture
  - education
excerpt: >
  Slides and recording from Teardown Portland 2025: a data-driven case that the
  super loop has a much bigger place in multitasking firmware than we give it credit
  for — and that preemptive RTOSes carry real costs worth examining.
documents:
  - title: "Slides (PDF)"
    url: /assets/teardown25_you_dont_need_an_rtos/you_dont_need_an_rtos.pdf
    type: pdf
---

*Long talk given at [Teardown Portland 2025](https://www.crowdsupply.com/teardown/portland-2025/long-talk/you-dont-need-an-rtos), June 2025.*

{% include youtube.html id="I4VRN5M1k4Y" %}

I've been developing this argument across a blog series for a while, but Teardown 2025 was my first chance to make the full case in front of a live audience — and I'll admit I was more than a little nervous stepping up to that stage.

The premise is simple: preemptive RTOSes are the default assumption whenever embedded firmware needs to do more than one thing, but that default is rarely examined. The super loop gets shoved to the side as if it's only appropriate for blinky demos. I wanted to challenge that.

**Setting the stage: what schedulers actually do**

Any time your device has tasks — things triggered by events, timers, or sensor reads — you have a scheduling problem. The question isn't whether you need a scheduler; it's which one. A preemptive RTOS is one answer. A carefully designed super loop is another, and it's underrated.

**What we give up with a preemptive RTOS**

This was the part I wanted to spend the most time on, because I think engineers underestimate the costs. Preemptive scheduling introduces genuine complexity: priority inversion, deadlocks, data races, stack sizing for each task, and ISR-to-task synchronization primitives. These are solvable problems, but they're real problems. They require careful design, good tooling, and ongoing vigilance. None of that is free.

**Response time analysis**

The part I think surprises people most is the formal analysis. Using basic schedulability theory, you can calculate whether a set of tasks with known periods and worst-case execution times will meet their deadlines — and the super loop, with a little care in structuring task release points, can meet the same deadlines as a preemptive scheduler for a wide class of real workloads. I walked through a worked example showing this on the whiteboard.

The key insight: for tasks without tight jitter requirements, the super loop's cooperative yield points can be placed deliberately to guarantee response times. The scheduler isn't magic; it's math. And that math applies equally well to a cooperative design.

**The case for keeping it simple**

My conclusion wasn't "never use an RTOS." It was: understand what you're getting and what you're giving up, and don't reach for the more complex tool by default. For a lot of firmware — including a surprising amount of what I've seen in production — the super loop is the right answer. The RTOS earns its complexity when you have hard real-time constraints that a cooperative design genuinely can't meet. Until then, keep it simple.

The audience had great questions afterward, including one about PID loops and jitter — which is exactly the right example of where you might actually need tighter scheduling guarantees. That's the kind of nuance I hope the talk opened up.

If you prefer reading to watching, this talk is the live version of my four-part EmbeddedRelated series: [Part 1](https://www.embeddedrelated.com/showarticle/1636.php), [Part 2](https://www.embeddedrelated.com/showarticle/1652.php), [Part 3](https://www.embeddedrelated.com/showarticle/1653.php), [Part 4](https://www.embeddedrelated.com/showarticle/1662.php). The articles cover the same material in considerably more depth.

[Session page →](https://www.crowdsupply.com/teardown/portland-2025/long-talk/you-dont-need-an-rtos)
