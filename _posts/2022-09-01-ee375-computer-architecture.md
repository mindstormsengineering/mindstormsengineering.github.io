---
layout: post
title: "EE375: Computer Architecture (West Point)"
date: 2022-09-01
type: tutorial
subjects:
  - digital-design
  - teaching
venue: West Point
excerpt: >
  A complete undergraduate computer architecture course built around the LC-3
  and designed to take students from logic gates all the way to a working 16-bit
  computer with I/O and interrupt handling — now freely available online.
---

*Course materials for EE375, taught at West Point and [published in full online](https://sites.google.com/view/ee375-computer-architecture).*

{% include youtube.html id="_0w27fvNveI" %}

Most computer architecture courses start from the instruction set and work outward. This one started from the gate and worked up. The goal was for students to finish the semester understanding not just how to program a computer, but how a computer actually works — from transistors to I/O handlers — with no hand-waving at any layer.

**Course structure**

The course was organized into six units:

- **Unit 0: Intro to EE375.** An introduction to the "Modern Classrooms" approach taken by the course, as well as course objectives, materials, assignments, and grading policy.
- **Unit 1: Intro to Computing and the LC-3.** Review of digital logic fundamentals (combinational logic flip-flops, registers, etc) and how they can be composed into a von Neumann computer. Describes the instruction set architecture (ISA) and simplified datapath for the "LC-3", the examplar 16-bit computer from *Introduction to Computing Systems* by Patt & Patel (which serves as the text for Units 0–4).
- **Unit 2: Assembly Language Programming.** How to write and debug assembly language programs (generally and in LC-3 assembly language) and how to compose things like subroutines, stacks, strings, and queues in assembly language.
- **Unit 3: Hardware Support for Input/Output and High-level Languages.** How memory-mapped IO (input/output) allows the LC-3 to interact with screens and keyboards using only memory reads and writes, including how those devices can "interrupt" the processor to have a condition immediately serviced by the processor. How the LC-3 controls access to the hardware using privilege and priority.
- **Unit 4: Completing the LC-3.** Description of the control system in the LC-3 and a full specification of the controller and datapath.
- **Unit 5: Performance Improvements.** Caches, pipelines, and a smattering of even more advanced designs (superscalar, out-of-order execution), using *Basic Computer Architecture* by Bhatt as the text. (partially completed)
- **Unit 6: Microcontrollers and Microprocessors.** A comparison of the LC-3 against more complex real-world architectures. (uncompleted)

**What made it different**

The course was deliberately bottom-up and cumulative. By Unit 4, students weren't reading about a datapath — they were building one, connecting the components they had studied in Units 0–3. The I/O and interrupt material in Unit 3 was similarly grounded: the hardware mechanisms for servicing an interrupt aren't mysterious once you've already built the datapath that has to save and restore state.

The LC-3 is simple enough to hold in your head all at once, which makes it an ideal teaching architecture. Students could trace a single instruction from fetch through execute and see exactly where in the circuit each thing happened. That kind of end-to-end clarity is hard to achieve with a real-world ISA.

**Availability**

All course materials — slides, notes, and assignments — are freely available at the link below. Unit 5 and Unit 6 were not completed before the course ended.

[View the full course →](https://sites.google.com/view/ee375-computer-architecture)
