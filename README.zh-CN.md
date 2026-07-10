<div align="center">
  <h1>UWB Project</h1>
  <p>面向 Mother-Ship 对接系统的 UWB 测距、三边定位、ESP32-S3 固件和可视化实验仓库。</p>

  <p>
    <a href="README.md">English</a>
    &middot;
    <a href="#快速开始">快速开始</a>
    &middot;
    <a href="#技术栈">技术栈</a>
    &middot;
    <a href="https://github.com/Ha22yX/Mother-Ship-Docking-Drone-System">主项目</a>
    &middot;
    <a href="https://github.com/Ha22yX/OpenMV-AprilTag">视觉模块</a>
    &middot;
    <a href="https://isef.rosebeg.com">项目网站</a>
  </p>

  <p>
    <img alt="Arduino: ESP32-S3" src="https://img.shields.io/badge/Arduino-ESP32-S3-00878F?style=for-the-badge&logo=arduino&logoColor=white" />
    <img alt="UWB: trilateration" src="https://img.shields.io/badge/UWB-trilateration-287866?style=for-the-badge" />
    <img alt="Pixhawk: MAVLink" src="https://img.shields.io/badge/Pixhawk-MAVLink-2f6f67?style=for-the-badge" />
    <img alt="Status: bench tests" src="https://img.shields.io/badge/Status-bench%20tests-6b7f73?style=for-the-badge" />
  </p>
</div>

<p align="center">
  <img src=".github/assets/readme-hero.svg" alt="UWB Project 项目概览图" width="100%" />
</p>

## 项目价值

当 GPS 精度不足以支撑对接时，母机和子机需要一个局部相对位置估计。本仓库专注 UWB 层，用于估计子机相对对接框架的偏移。

## 快速开始

```bash
git clone https://github.com/Ha22yX/UWB-Project.git
cd UWB-Project
pip install -r tools/requirements.txt
# 在 Arduino IDE 中打开 firmware/uwb/uwb_tag_solver 进行 ESP32-S3 测试
python tools/visualization/uwb_viewer.py
```

运行可视化工具或烧录固件前，请根据本地硬件修改串口和 UWB ID。

## 核心功能

- 四锚点 UWB 布局，用于母机坐标系下的相对定位。
- ESP32-S3 草图覆盖测距、标签解算、ESP-NOW 和 Pixhawk 实验。
- 包含中值滤波与最小二乘三边定位实验。
- 提供 Python 串口调试和姿态可视化工具。

## 技术栈

| Layer | Technology | Role |
| --- | --- | --- |
| 固件 | Arduino / ESP32-S3 | UWB、ESP-NOW 与 MAVLink 侧实验。 |
| 定位 | UWB 三边定位 | 把锚点距离转换为局部 x/y/z 估计。 |
| 可视化 | PyQtGraph, matplotlib, pyserial | 查看位姿流与串口输出。 |
| 集成 | Pixhawk / MAVLink | 飞控通信台架测试。 |


## 项目说明

这是 [Mother-Ship-Docking-Drone-System](https://github.com/Ha22yX/Mother-Ship-Docking-Drone-System) 的附属仓库，负责 UWB 定位模块；[OpenMV-AprilTag](https://github.com/Ha22yX/OpenMV-AprilTag) 负责近距离视觉定位模块。


## 项目结构

```text
firmware/uwb/        UWB ranging and solver sketches
firmware/docking/    mother/child ESP-NOW docking sketches
tools/visualization/ serial and 3D viewers
docs/                notes, references, and diagrams
```
