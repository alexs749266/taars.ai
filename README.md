# TAARS — Trigger AI Alert Relay System

**An autonomous, event-driven underwater buoy that detects a physical disturbance, surfaces on its own, and sends a geolocated alert.**

[![Pool Demo](https://img.shields.io/badge/Demo-Jerk%20Trigger-blue.svg)](https://youtu.be/QN2yup6PBXI)
[![Sea Trial](https://img.shields.io/badge/Field%20Test-Sea%20Trial-green.svg)](https://youtu.be/AlvjGmI3BEE)
[![Website](https://img.shields.io/badge/Web-taars.ai-blue.svg)](https://taars.ai)

> **Status:** Proof-of-concept prototype. Built and field-tested in open-sea conditions. This repository documents the project honestly at its current early stage — see [What's proven vs. what's next](#whats-proven-vs-whats-next).

---

## The idea

Most underwater monitoring relies on cables, permanent moorings, or always-on sensor networks. These are expensive to deploy, power-hungry, and hard to scale across a wide area.

TAARS takes a different approach: a small buoy rests on the seabed in a **low-power standby state** and does nothing until it detects a significant physical disturbance. On a trigger, it releases its ballast, floats to the surface, gets a GPS fix, connects over the cellular network, and sends an alert with its location.

```
Seabed standby  →  Jerk trigger  →  Ballast release  →  Surface  →  GPS + GSM  →  Alert
```

---

## How it works

**Jerk Trigger.** The unit watches the *rate of change* of acceleration ("jerk") rather than acceleration alone. This helps separate abrupt, high-energy events from the gentle motion of waves and currents, while keeping the device in a low-power state until something real happens.

**Self-surfacing.** When the trigger fires, a Bluetooth-controlled relay deactivates an electromagnet that was holding the ballast. The unit becomes positively buoyant and rises to the surface on its own — no motors.

**Alert delivery.** At the surface, the onboard smartphone acquires a GPS fix, connects over cellular, and pushes an alert to a Telegram bot with the coordinates and a map link. (See the screenshot in the technical materials.)

---

## Prototype at a glance

This is an early experimental unit built from off-the-shelf and repurposed parts. The numbers below describe the **current prototype as built**, and are expected to change as the design matures.

| Parameter | Value (current prototype) |
|---|---|
| Height | 48 cm |
| Diameter | ~90 mm (nose / fairing), ~80 mm (main body) |
| Weight | ~2.5 kg in air |
| Housing | Sealed, pressure-resistant housing (repurposed / COTS) |
| Compute | Compact Android smartphone running a custom in-house app |
| Sensing | 3-axis accelerometer; Jerk Trigger detection |
| Actuation | 2-channel Bluetooth relay (ballast electromagnet + LED beacon) |
| Power | Battery pack with step-down / step-up converters |
| Communication | GPS + GSM via the smartphone; Telegram alert delivery |
| Tested depth | ~5 m (open-sea, limited by free-dive filming — not a housing depth limit) |
| Motors | None (buoyancy-driven ascent) |

> **Note:** the test unit carried a minimal battery sufficient only for functional testing. Endurance and maximum depth rating were not goals of the initial trials — the goal was to confirm the full sequence works end to end.

---

## What's proven vs. what's next

**Demonstrated on the prototype:**

- Electromagnetic ballast retention and release via the Bluetooth relay
- Controlled, motor-free surfacing
- Waterproof enclosure performance in the ocean
- Timer-based and command-based activation
- Preliminary Jerk Trigger detection (tested with the logic on and off)
- LED beacon operation after surfacing
- Automated Telegram alert delivery with live GPS coordinates

**Not yet done — future R&D:**

- Scientific validation of specific event types (e.g. seismic detection)
- Long-duration deployment and endurance characterization
- Depth-rating qualification of the housing
- Communication / antenna reliability improvements after surfacing
- Migration from a smartphone to dedicated low-power hardware
- Multi-unit / networked operation

---

## Technology stack

**Hardware:** Android smartphone (compute + GPS + GSM), 3-axis accelerometer, 2-channel Bluetooth relay, ballast electromagnet, LED beacon, battery with DC converters, sealed pressure-resistant housing.

**Software:** custom Android application that monitors the accelerometer, evaluates the Jerk Trigger condition, drives the relay channels, logs data, and sends Telegram alerts. The unit can also be commanded through Telegram during testing.

---

## Applications

TAARS is aimed at public-sector and infrastructure operators responsible for coastal monitoring, for example:

- Disaster-monitoring and early-warning agencies
- Port authorities and maritime infrastructure operators
- Coastal emergency-management organizations
- Marine and environmental research institutions

These are target applications for a matured system, not claims about the current prototype.

---

## The longer-term vision

The name carries the original ambition: a **swarm** of low-cost passive sentinels deployed across an area, eventually coordinating with each other (for example over acoustic links) to localize and confirm events as a network.

That swarm capability is a **long-term research direction, not a current feature.** Today TAARS is a single, working, sea-tested unit. The path is: one proven node → many units across an area → a coordinated network.

---

## Media & links

- **Pool demo (Jerk Trigger):** https://youtu.be/QN2yup6PBXI
- **Sea trial (timed surfacing):** https://youtu.be/AlvjGmI3BEE
- **Website:** https://taars.ai

---

## Contact

**Aleksandr Shakhov** — Founder, Taars Technologies LLC (Delaware, USA)

- Email: aleksandr@taars.ai
- Website: https://taars.ai
- LinkedIn: https://www.linkedin.com/company/taars-technologies-llc

---

*© 2026 Taars Technologies LLC. This repository documents an experimental proof-of-concept; specifications and design are subject to change during ongoing R&D.*
