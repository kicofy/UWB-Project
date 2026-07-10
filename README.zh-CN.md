<div align="center">
  <h1>UWB Project</h1>
  <p>面向 Mother-Ship 对接系统的 UWB 测距、三边定位、ESP32-S3 固件和可视化实验仓库。</p>

  <p>
    <a href="README.md">English</a>
    &middot;
    <a href="https://github.com/Ha22yX/Mother-Ship-Docking-Drone-System">主项目</a>
    &middot;
    <a href="https://github.com/Ha22yX/OpenMV-AprilTag">视觉模块</a>
    &middot;
    <a href="https://isef.rosebeg.com">项目网站</a>
    &middot;
    <a href="#快速开始">快速开始</a>
    &middot;
    <a href="#技术栈">技术栈</a>
  </p>

  <p>
    <img alt="Arduino: ESP32-S3" src="https://img.shields.io/badge/Arduino-ESP32--S3-00878F?style=for-the-badge&logo=arduino&logoColor=white" />
    <img alt="UWB: trilateration" src="https://img.shields.io/badge/UWB-trilateration-287866?style=for-the-badge" />
    <img alt="Pixhawk: MAVLink" src="https://img.shields.io/badge/Pixhawk-MAVLink-2f6f67?style=for-the-badge" />
    <img alt="Status: bench tests" src="https://img.shields.io/badge/Status-bench%20tests-6b7f73?style=for-the-badge" />
  </p>
</div>

<p align="center">
  <img src=".github/assets/readme-hero.svg" alt="UWB Project 项目概览图" width="100%" />
</p>

## 项目价值

这个仓库负责对接项目中的中距离相对位置层。GPS 可以让两架无人机接近，但对接需要母机坐标系下的位置估计。UWB 测距提供这个局部信号，再交给末端视觉进一步对准。

## 工作流

- 在母机对接框架上放置 UWB 锚点，在子无人机上放置标签。
- 通过 ESP32-S3 串口实验读取 UWB 距离数据。
- 对每个锚点距离做滤波，降低跳变影响。
- 使用三边定位/最小二乘实验解算局部 `x, y, z`。
- 通过可视化工具查看位姿流，并为 Pixhawk/MAVLink 集成做准备。

## 核心功能

- ESP32-S3 Arduino 草图覆盖 UWB 测距、标签解算、ESP-NOW 和 Pixhawk 实验。
- 面向对接框架的四锚点相对定位几何。
- Python 串口查看器和 3D 可视化工具。
- 作为 Mother-Ship 主项目的 UWB 定位附属仓库。

## 快速开始

```bash
git clone https://github.com/Ha22yX/UWB-Project.git
cd UWB-Project
pip install -r tools/requirements.txt
# Flash the ESP32-S3 sketches from firmware/ in Arduino IDE
python tools/visualization/uwb_viewer.py
```

运行可视化工具或烧录固件前，请先根据本地硬件修改串口、UWB ID 和几何尺寸。

## 技术栈

| 层级 | 技术 | 作用 |
| --- | --- | --- |
| 固件 | Arduino / ESP32-S3 | UWB、ESP-NOW 与 Pixhawk 侧实验。 |
| 定位 | UWB 三边定位 | 把锚点距离转换为局部相对位置。 |
| 可视化 | PyQtGraph, matplotlib, pyserial | 查看串口输出和位姿流。 |
| 集成 | Pixhawk / MAVLink | 台架测试飞控通信路径。 |

## 项目结构

```text
firmware/uwb/             UWB ranging and solver sketches
firmware/docking/         mother/child ESP-NOW docking sketches
firmware/pixhawk/         Pixhawk TELEM and MAVLink experiments
tools/visualization/      serial and 3D viewers
docs/                     notes, references, and diagrams
```

## 项目说明

这是硬件/固件实验工作区，不是可直接飞行的飞控软件包。
