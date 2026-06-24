---
layout: post
title: "Build HackerBox #0040 and Wield the PIC of Destiny! (Teardown 2023)"
date: 2023-06-25
type: tutorial
subjects:
  - hardware
  - firmware
  - education
excerpt: >
  Workshop materials from Teardown Portland 2023: guided assembly and programming
  of HackerBox #0040, a PIC microcontroller kit with a PICkit 3 programmer, LCD
  display, and GPS module.
documents:
  - title: "Workshop Worksheet (PDF)"
    url: /assets/teardown23_PIC_of_destiny/Hackerbox_0040_Worksheet_v2.pdf
    type: pdf
---

*Workshop given at [Teardown Portland 2023](https://www.crowdsupply.com/teardown/portland-2023/workshop/build-hackerbox-0040-and-wield-the-pic-of-destiny), June 2023.*

HackerBox #0040 is a kit built around PIC microcontrollers — specifically a PIC16F628 and a PIC12F675, alongside a PICkit 3 programmer with ZIF socket, a 16x2 LCD display, a GPS module with antenna, and a breadboard full of supporting components. This workshop was as much about working through a real hardware kit as about any specific skill: build first, understand as you go.

**What's in the kit**

The PICkit 3 programmer includes a ZIF (zero insertion force) socket for easy chip swapping — an underrated convenience when people are touching hardware for the first time and not all contact is gentle. The breadboard power supply is USB-powered, which removes a common stumbling block at live events. The GPS module adds a practical application layer that motivates the peripheral work: reading NMEA sentences from a GPS receiver is a satisfying first embedded I/O project.

**What the workshop covered**

We worked through the worksheet together: getting the toolchain installed, getting the PICkit 3 recognized, and loading the first program. From there, participants worked through exercises covering the key peripheral categories — power supply and clocking configuration, in-circuit programming and debugging with the PICkit 3, interfacing the MCU to the LCD display, and, for those who got there, reading NMEA data from the GPS receiver.

The worksheet was designed to be completable independently after the session. Most workshops leave you with a half-built thing and no clear path forward; the goal here was that participants could continue working through the kit on their own after Teardown ended.

**Reading PIC documentation**

I made a point of grounding the session in the PIC's documentation ecosystem: the datasheet, the family reference manual, and the MPLAB X IDE help system. One of the subtle skills in embedded development is knowing which document answers which question. The PIC family's documentation is thorough and well-organized, making it a reasonable first experience with professional-grade MCU reference material.

- [HackerBox #0040 product page →](https://hackerboxes.com/products/hackerbox-0040-pic-of-destiny)
