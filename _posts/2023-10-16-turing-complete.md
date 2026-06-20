---
layout: post
title: "What Does It Mean to Be \"Turing Complete\"?"
date: 2023-10-16
type: article
subjects:
  - education
excerpt: >
  A tour through Alan Turing's 1936 thought experiments — what a "Turing
  machine" is, why it matters, and what it actually means when a programming
  language or system is called "Turing complete."
---

*Originally published on [EmbeddedRelated](https://www.embeddedrelated.com/showarticle/1588.php).*

![Portrait of Alan Turing]({{ '/assets/turing_complete/alan_turing.jpg' | relative_url }})

What does it mean for something to be "Turing complete" — and why does it matter? The term traces back to 1936, before the first computer had been built, when mathematician Alan Turing was asking a foundational question: what are the theoretical capabilities and limitations of machines that perform mathematical operations? To answer it, Turing imagined an abstract machine — now called a Turing machine — capable of reading and writing symbols on an infinite tape according to a finite set of rules. Despite its conceptual simplicity, such a machine can compute anything that is computable at all.

A system is called "Turing complete" if it can simulate a Turing machine, meaning it has the same theoretical computational power. The practical implication is that nearly every modern programming language is Turing complete — they can all express the same set of algorithms, just with different amounts of effort. What makes this counterintuitive is that some famously minimal systems (Conway's Game of Life, make, even the x86 MOV instruction by itself) are also Turing complete, while purposely limited systems like regular expressions are not.

The article grounds this in the broader history of computational theory — including Big O notation, NP-completeness, and the historical context of visionaries in the 1930s who were simultaneously building the first mechanical computers and asking deep theoretical questions about what machines could ever do. A useful primer for anyone who has heard the term and wondered what it actually means.

[Read the full article →](https://www.embeddedrelated.com/showarticle/1588.php)
