---
layout: post
title: "Why is This Code Bad?"
date: 2025-10-08
type: article
subjects:
  - firmware
venue: DigiKey
excerpt: >
  A Python function for parsing GCC dependency files becomes a case study in
  what separates "barely working" code from simple code — and why simplicity is
  worth pursuing deliberately.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/maker/tutorials/2025/why-is-this-code-bad).*

![A spectrum from broken code to simple, elegant code]({{ '/assets/bad_code/BadCode_10_Spectrum5.png' | relative_url }})

The article opens with two implementations of the same function — one sprawling, one concise — and asks why the shorter one feels easier to work with, not just shorter. The answer leads to a "spectrum of badness" from "doesn't work" through "barely working spaghetti" to "simple and correct," with cyclomatic complexity and unnecessary abstraction as the two main drags on code quality.

The case study is a real function: parsing GCC `.d` dependency files to extract a list of file paths. The first solution had a subtle bug (mutating a list while iterating over it), and fixing it revealed a simpler framing of the whole problem — read the file as one string, replace newlines with spaces, split on spaces, filter for valid paths. The result is shorter, has no mutation hazard, and is easier to reason about.

When a simple solution isn't available, structured refactorings (Extract Method, Replace Conditional with a Look-up Table) keep complexity manageable. When complexity is unavoidable, comments that show concrete input/output examples and accompanying flowcharts are more useful than prose descriptions — and a unit test is worth more than either.

[Read the full article →](https://www.digikey.com/en/maker/tutorials/2025/why-is-this-code-bad)
