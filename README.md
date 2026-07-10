<div align="center">
  <h1>UWB Project</h1>
  <p>UWB ranging, trilateration, ESP32-S3 firmware, and visualization for the Mother-Ship docking system.</p>

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

## Why This Exists

This repository owns the mid-range relative-position layer of the docking project. GPS can bring two UAVs close, but docking needs a mother-frame position estimate. UWB ranges provide that local signal before terminal vision takes over.

## Workflow

- Place UWB anchors on the mother docking frame and a tag on the child UAV.
- Read distance lines from the UWB hardware through ESP32-S3 serial experiments.
- Filter per-anchor distances to reduce spikes.
- Solve local `x, y, z` with trilateration/least-squares experiments.
- Visualize the pose stream and prepare the estimate for Pixhawk/MAVLink integration.

## Features

- ESP32-S3 Arduino sketches for UWB ranging, tag solving, ESP-NOW, and Pixhawk experiments.
- Four-anchor relative-localization geometry for a docking frame.
- Python serial viewers and 3D visualization tools.
- Clear companion role for the main Mother-Ship project.

## Quickstart

```bash
git clone https://github.com/Ha22yX/UWB-Project.git
cd UWB-Project
pip install -r tools/requirements.txt
# Flash the ESP32-S3 sketches from firmware/ in Arduino IDE
python tools/visualization/uwb_viewer.py
```

Update serial ports, UWB IDs, and hardware geometry before running viewers or flashing firmware.

## Tech Stack

| Layer | Technology | Role |
| --- | --- | --- |
| Firmware | Arduino / ESP32-S3 | UWB, ESP-NOW, and Pixhawk-side experiments. |
| Localization | UWB trilateration | Convert anchor ranges into local relative position. |
| Visualization | PyQtGraph, matplotlib, pyserial | Inspect serial output and pose streams. |
| Integration | Pixhawk / MAVLink | Bench-test flight-controller communication paths. |

## Project Map

```text
firmware/uwb/             UWB ranging and solver sketches
firmware/docking/         mother/child ESP-NOW docking sketches
firmware/pixhawk/         Pixhawk TELEM and MAVLink experiments
tools/visualization/      serial and 3D viewers
docs/                     notes, references, and diagrams
```

## Notes

This repo is a hardware/firmware experiment workspace, not a finished flight-control package.
