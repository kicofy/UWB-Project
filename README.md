<div align="center">
  <h1>UWB Project</h1>
  <p>UWB ranging, trilateration, ESP32-S3 firmware, and visualization for the Mother-Ship docking system.</p>

  <p>
    <a href="README.zh-CN.md">Chinese</a>
    &middot;
    <a href="#quickstart">Quickstart</a>
    &middot;
    <a href="#tech-stack">Tech Stack</a>
    &middot;
    <a href="https://github.com/Ha22yX/Mother-Ship-Docking-Drone-System">Main Project</a>
    &middot;
    <a href="https://github.com/Ha22yX/OpenMV-AprilTag">Vision Module</a>
    &middot;
    <a href="https://isef.rosebeg.com">Project Website</a>
  </p>

  <p>
    <img alt="Arduino: ESP32-S3" src="https://img.shields.io/badge/Arduino-ESP32-S3-00878F?style=for-the-badge&logo=arduino&logoColor=white" />
    <img alt="UWB: trilateration" src="https://img.shields.io/badge/UWB-trilateration-287866?style=for-the-badge" />
    <img alt="Pixhawk: MAVLink" src="https://img.shields.io/badge/Pixhawk-MAVLink-2f6f67?style=for-the-badge" />
    <img alt="Status: bench tests" src="https://img.shields.io/badge/Status-bench%20tests-6b7f73?style=for-the-badge" />
  </p>
</div>

<p align="center">
  <img src=".github/assets/readme-hero.svg" alt="UWB Project overview image" width="100%" />
</p>

## Why This Exists

The mother drone and child drone need a local position estimate when GPS is not precise enough for docking. This repo focuses on the UWB layer that estimates the child drone's offset from the docking frame.

## Quickstart

```bash
git clone https://github.com/Ha22yX/UWB-Project.git
cd UWB-Project
pip install -r tools/requirements.txt
# Open firmware/uwb/uwb_tag_solver in Arduino IDE for ESP32-S3 tests
python tools/visualization/uwb_viewer.py
```

Hardware serial ports and UWB IDs must match your local setup before running viewers or flashing firmware.

## Features

- Four-anchor UWB layout for mother-frame relative localization.
- ESP32-S3 sketches for ranging, tag solving, ESP-NOW, and Pixhawk experiments.
- Median filtering and least-squares trilateration experiments.
- Python viewers for serial debugging and pose visualization.

## Tech Stack

| Layer | Technology | Role |
| --- | --- | --- |
| Firmware | Arduino / ESP32-S3 | UWB, ESP-NOW, and MAVLink-side experiments. |
| Localization | UWB trilateration | Convert anchor distances into local x/y/z estimates. |
| Visualization | PyQtGraph, matplotlib, pyserial | Inspect pose streams and serial output. |
| Integration | Pixhawk / MAVLink | Bench tests for flight-controller communication. |


## Project Notes

This is a companion repository for [Mother-Ship-Docking-Drone-System](https://github.com/Ha22yX/Mother-Ship-Docking-Drone-System). It owns the UWB positioning module; [OpenMV-AprilTag](https://github.com/Ha22yX/OpenMV-AprilTag) owns the close-range visual localization module.


## Project Map

```text
firmware/uwb/        UWB ranging and solver sketches
firmware/docking/    mother/child ESP-NOW docking sketches
tools/visualization/ serial and 3D viewers
docs/                notes, references, and diagrams
```
