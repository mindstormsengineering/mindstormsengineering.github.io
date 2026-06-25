---
layout: post
title: "Can an ADC Be Just a Random Number Generator?"
date: 2025-10-22
type: article
subjects:
  - hardware
venue: DigiKey
excerpt: >
  A 16-bit ADC doesn't always give you 16 bits of useful information — noise can
  reduce effective resolution dramatically. This article shows how to measure it
  and recover lost bits through oversampling, averaging, and filtering.
---

*Originally published on [Maker.io (DigiKey)](https://www.digikey.com/en/articles/can-an-adc-be-just-a-random-number-generator).*

![ADC noise floor characterization setup]({{ '/assets/adc_is_a_rng/14_Screenshot2024-11-14083239.png' | relative_url }})

"A lot of 16-bit ADCs really operate as 7-bit ADCs and 9-bit random number generators." ADC noise means that repeated samples of a stable reference voltage don't all return the same code — they form a distribution. How wide that distribution is determines how many bits of your ADC's resolution are actually carrying signal versus noise.

The measurement procedure is straightforward: connect a low-noise voltage reference (noise floor less than ⅓ of expected ADC noise) and take many samples. The standard deviation of the resulting distribution gives the noise in LSBs, which maps directly to effective number of bits (ENOB). The article then covers practical techniques to recover those lost bits: oversampling and decimation, running averages, and low-pass filtering. Gain, offset, and differential nonlinearity errors — which remain even after noise is suppressed — are flagged as a separate follow-on topic.

[Read the full article →](https://www.digikey.com/en/articles/can-an-adc-be-just-a-random-number-generator)
