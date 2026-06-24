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

The premise: preemptive RTOSes are the default assumption whenever embedded firmware needs to do more than one thing at a time, but that default rarely gets examined. The super loop gets dismissed as only appropriate for simple programs, while the RTOS gets adopted before anyone has asked whether it's actually needed. This talk makes the case, with math, that the super loop is underrated.

**What you give up with a preemptive RTOS**

Preemptive scheduling introduces a category of bugs that simply don't exist in cooperative designs: data races, priority inversion, and deadlocks. Shared state that looks fine in a single-threaded context becomes a source of non-deterministic failures as soon as a higher-priority task can preempt at any instruction boundary. Each task also needs its own stack, sized for its worst-case call depth — which is often a guess. These are solvable problems, but they're real ones that require ongoing care.

**Schedulability analysis**

The more interesting question is whether a super loop can actually meet timing requirements that you'd otherwise reach for an RTOS for. The answer comes from response time analysis. For any task *i* in a preemptive system, its worst-case response time R_i satisfies:

R_i = C_i + Σ_{j ∈ hp(i)} ⌈R_i / T_j⌉ · C_j

where C_i is task i's worst-case execution time, T_j is the period of each higher-priority task j, and hp(i) is the set of tasks with higher priority than i. The sum accounts for how many times each higher-priority task can preempt i during i's own response time — including interrupts. This equation is solved iteratively, and the task meets its deadline if R_i ≤ D_i.

The talk works through a concrete example on the slides — a set of tasks with known periods and worst-case execution times — showing how to compute whether the task set is schedulable. The key result: with deliberate placement of cooperative yield points, a super loop can satisfy the same response time constraints as a preemptive scheduler for a wide class of real workloads. The scheduler isn't magic; it's math, and that math applies equally to cooperative designs.

**The conclusion**

An RTOS earns its complexity when you have hard real-time requirements that genuinely can't be met cooperatively — tight jitter on a PID loop being the clearest example. Until then, the super loop is often the right tool: simpler to reason about, easier to analyze, and free of an entire class of concurrency bugs.

If you prefer reading to watching, the first two parts of my EmbeddedRelated series cover this same ground in more depth: [Part 1](https://www.embeddedrelated.com/showarticle/1636.php), [Part 2](https://www.embeddedrelated.com/showarticle/1652.php). Parts [3](https://www.embeddedrelated.com/showarticle/1653.php) and [4](https://www.embeddedrelated.com/showarticle/1662.php) go further than the talk does.

[Session page →](https://www.crowdsupply.com/teardown/portland-2025/long-talk/you-dont-need-an-rtos)
