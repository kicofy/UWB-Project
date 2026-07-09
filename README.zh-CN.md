# UWB-Project 中文说明

本仓库的默认 [README.md](README.md) 已经改为完整中文说明，并包含英文摘要。请优先阅读 `README.md`，其中详细介绍了：

- 本仓库与主项目 [Mother-Ship-Docking-Drone-System](https://github.com/Ha22yX/Mother-Ship-Docking-Drone-System) 的关系。
- UWB 在双无人机空中对接系统中的作用。
- 4 anchor + 1 tag 的相对位置获取方案。
- anchor 坐标系、测距输出、中值滤波、三边定位和 `z` 轴镜像解。
- ESP32-S3、Pixhawk/PX4、MAVLink、ESP-NOW 和 OpenMV/AprilTag 的集成方式。
- 固件目录、Python 可视化工具、接线方式、测试流程和安全注意事项。

项目介绍网站：[https://isef.rosebeg.com](https://isef.rosebeg.com)

主项目仓库：[Ha22yX/Mother-Ship-Docking-Drone-System](https://github.com/Ha22yX/Mother-Ship-Docking-Drone-System)

当前仓库负责主项目中的 UWB 测距、相对定位和嵌入式测试部分；主仓库负责系统总体说明、GPS/PX4/UDP 通信实验和双无人机对接流程说明。
