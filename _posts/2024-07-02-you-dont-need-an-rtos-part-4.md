---
layout: post
title: "You Don't Need an RTOS (Part 4)"
date: 2024-07-02
type: article
subjects:
  - firmware
  - architecture
venue: EmbeddedRelated
excerpt: >
  The concluding installment: implementing mailboxes, queues, counting
  semaphores, and the Observer pattern on top of the Superduperloop, plus
  a dispatch-queue scheduler — completing the full picture of DIY IPC.
---

*Originally published on [EmbeddedRelated](https://www.embeddedrelated.com/showarticle/1662.php).*

![Inter-process communication methods comparison table]({{ '/assets/rtos_p4/ipc_table.png' | relative_url }})

Part 4 finishes the IPC taxonomy started in Part 3. Mailboxes, queues, counting semaphores, the Observer pattern, and a construct that I call a "marquee" round out the set of mechanisms tasks need to communicate reliably — all implemented without a preemptive RTOS. The article walks through each one in enough detail to implement it, including how to post arbitrary data types and pointers to a mailbox and how to analyze the schedulability impact of adding a queue.

A second major addition is the dispatch queue: an alternative non-preemptive scheduler in which tasks are posted as function pointers to a central queue and executed in EDF (earliest deadline first) order. This is conceptually simple to understand but significantly more challenging to analyze for determining schedulability than any other technique discussed thus far. The tradeoff is that it handles certain difficult task sets that the Superduperloop cannot, which makes it a useful complementary tool.

The article closes with a full summary of the four-part series — what schedulability analysis tells you, when the Superduperloop suffices, when to reach for one of the off-the-shelf cooperative schedulers from Part 3, and when a preemptive RTOS is actually justified. The core takeaway: the RTOS should be the last tool you reach for, not the first.

**Additional Resources**

- [You Don't Need an RTOS (Teardown 2025)]({% post_url 2025-06-21-teardown25-you-dont-need-an-rtos %}) — a talk covering the schedulability analysis and the case for cooperative scheduling

[Read the full article →](https://www.embeddedrelated.com/showarticle/1662.php)
