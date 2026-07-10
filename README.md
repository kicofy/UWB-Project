<div align="center">
  <h1>UWB Project</h1>
  <p>UWB ranging, trilateration, ESP32-S3 firmware, and visualization for a mother-ship UAV docking system.</p>

  <p>
    <a href="README.zh-CN.md">Chinese</a>
    &middot;
    <a href="https://github.com/Ha22yX/Mother-Ship-Docking-Drone-System">Main Project</a>
    &middot;
    <a href="https://github.com/Ha22yX/OpenMV-AprilTag">Vision Module</a>
    &middot;
    <a href="https://isef.rosebeg.com">Project Website</a>
    &middot;
    <a href="#quickstart">Quickstart</a>
    &middot;
    <a href="#features">Features</a>
    &middot;
    <a href="#tech-stack">Tech Stack</a>
  </p>

  <p>
    <img alt="Arduino: ESP32-S3" src="https://img.shields.io/badge/Arduino-ESP32--S3-00878F?style=for-the-badge&logo=arduino&logoColor=white" />
    <img alt="UWB: trilateration" src="https://img.shields.io/badge/UWB-trilateration-287866?style=for-the-badge" />
    <img alt="Pixhawk: MAVLink" src="https://img.shields.io/badge/Pixhawk-MAVLink-2f6f67?style=for-the-badge" />
    <img alt="Status: bench tests" src="https://img.shields.io/badge/Status-bench%20tests-6b7f73?style=for-the-badge" />
  </p>
</div>

<p align="center">
  <img src=".github/assets/readme-hero.svg" alt="UWB Project overview image" width="100%" />
</p>

## Overview

This repository owns the mid-range relative-position layer of the Mother-Ship Docking Drone System. GPS/RTK can bring the child UAV near the mother platform, but docking needs a local coordinate estimate relative to the mother frame.

The experiments here focus on turning UWB anchor-to-tag ranges into an inspectable `x, y, z` estimate, then preparing that estimate for Pixhawk/MAVLink and the larger docking stack.

## Features

- ESP32-S3 Arduino sketches for UWB ranging, ESP-NOW, and Pixhawk-side communication experiments.
- Four-anchor docking-frame geometry for relative localization experiments.
- Trilateration and least-squares solving path for converting ranges into local position.
- Python serial tools and 3D viewers for inspecting distance and pose streams.
- Companion role to the main docking project, alongside the OpenMV AprilTag vision module.

## How It Works

1. Mount UWB anchors on the mother docking frame and a UWB tag on the child UAV.
2. Read per-anchor distance packets from the ESP32-S3/UWB hardware path.
3. Filter distance spikes and map ranges to the configured anchor geometry.
4. Solve the relative position estimate and visualize it on the PC tools.
5. Use the result as the mid-range localization signal before terminal vision alignment.

## Quickstart

Clone the repo, install the PC visualization dependencies, and flash the firmware from `firmware/` with Arduino IDE or your ESP32 toolchain.

```bash
git clone https://github.com/Ha22yX/UWB-Project.git
cd UWB-Project
pip install -r tools/requirements.txt
# Flash the ESP32-S3 sketches from firmware/ in Arduino IDE
python tools/visualization/uwb_viewer.py
```

Update serial ports, UWB IDs, anchor coordinates, and baud rates for your actual hardware before running the viewers.

## Configuration

| Item | What to adjust |
| --- | --- |
| Anchor geometry | Measure anchor positions on the mother docking frame and keep units consistent. |
| Serial ports | Set the ESP32-S3 / UWB / Pixhawk ports used by the viewer scripts. |
| UWB IDs | Match firmware anchor/tag IDs to the physical modules. |
| Flight-controller path | Treat MAVLink/Pixhawk scripts as bench tests until verified safely. |

## Tech Stack

| Layer | Technology | Role |
| --- | --- | --- |
| Firmware | Arduino, ESP32-S3 | UWB, ESP-NOW, and Pixhawk experiments. |
| Localization | UWB trilateration | Convert ranges into mother-frame relative position. |
| Visualization | pyserial, matplotlib, PyQtGraph | Inspect serial data and pose streams. |
| Integration | Pixhawk, MAVLink | Prepare flight-controller communication paths. |

## Project Layout

```text
firmware/uwb/             UWB ranging and solver sketches
firmware/docking/         mother/child ESP-NOW docking sketches
firmware/pixhawk/         Pixhawk TELEM and MAVLink experiments
tools/visualization/      serial and 3D viewers
docs/                     wiring notes, references, and diagrams
archive/                  older prototypes kept for context
```

## Status

Hardware research workspace. It is useful for bench testing and documentation, but it is not a ready-to-fly autopilot or safety-certified docking controller.

## Related Projects

- [Mother-Ship-Docking-Drone-System](https://github.com/Ha22yX/Mother-Ship-Docking-Drone-System) - main autonomous docking project.
- [OpenMV-AprilTag](https://github.com/Ha22yX/OpenMV-AprilTag) - terminal visual localization module.

## License

No project-wide open-source license has been declared yet.
