---
layout: post
title: "Make Your Own MCU Boards (Teardown 2023)"
date: 2023-06-25
type: talk
subjects:
  - hardware
  - pcb
  - education
excerpt: >
  Slides and recording from Teardown Portland 2023: the five things every MCU board
  needs, why the minimal circuit is simpler than you think, and how to source, lay
  out, and build your first breakout board.
documents:
  - title: "Notes (PDF)"
    url: /assets/teardown23_make_your_own_mcu_boards/Make-Your-Own-MCU-Boards_Notes.pdf
    type: pdf
  - title: "References and Resources (PDF)"
    url: /assets/teardown23_make_your_own_mcu_boards/References_and_Resources.pdf
    type: pdf
---

*Short talk given at [Teardown Portland 2023](https://www.crowdsupply.com/teardown/portland-2023/short-talk/make-your-own-mcu-boards), June 2023.*

{% include youtube.html id="P6SZerdCFyo" %}

The premise of this talk is something I genuinely believe: you don't need to keep buying expensive development boards. The minimal circuit for bringing up a microcontroller is pretty simple, and the information you need to design one is publicly available. The hardware reference guide for any MCU will walk you through it. If you can follow a schematic and solder, you're most of the way there.

**The five things every MCU board needs**

No matter the microcontroller, there are five fundamental concerns, and none require complex solutions:

1. **Power** — the MCU needs stable supply voltage, typically with decoupling capacitors close to each supply pin. The values aren't magic; the datasheet specifies them.

2. **Clocking** — most modern MCUs can use an internal oscillator right out of the box. An external crystal gives you better accuracy and lower jitter when your application needs it; a surprising number don't.

3. **Reset** — you need a reliable way to get the device into a known state. A pull-up resistor on the reset pin and an optional button covers almost every case.

4. **Programming** — how does code get onto the chip? Most MCUs support SWD, JTAG, or a UART bootloader, all requiring only a few pins and a simple header. Designing that header in costs essentially nothing.

5. **Specialty pins** — some MCUs have pins that must be in a specific state at boot to control operating mode (BOOT0 on STM32 devices, for example). The datasheet will tell you which ones and what they need.

**Sourcing, layout, and assembly**

I covered the hobbyist-friendly end of the stack: LCSC for components, KiCad for schematic capture and layout, and services like JLCPCB or OSHPark for fabrication. These aren't the only options, but they have low minimums, reasonable prices, and well-documented workflows.

I also touched briefly on the electrical constraints worth keeping in mind: making sure your supply voltage and current budget are right, and that signal traces are short enough that rise time doesn't cause problems. For most hobbyist designs running at moderate clock speeds, rise time isn't a crisis — but knowing it exists means you won't be surprised the first time it is.

The GitHub repo linked below is my own STM32F103C8T6 breakout board design, included as a reference. It's the simplest version of a real, working MCU board I could make.

- [STM32F103C8T6 breakout board (GitHub) →](https://github.com/nathancharlesjones/STM32F103C8T6-breakout-board)
- [Session page →](https://www.crowdsupply.com/teardown/portland-2023/short-talk/make-your-own-mcu-boards)
