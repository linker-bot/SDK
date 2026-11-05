# LinkerBot SDK 项目目录

LinkerBot 灵巧手、机械臂的 SDK、通信库与遥操作工具入口。
本仓库用于项目导航，请前往对应仓库安装和构建软件。

[English](README.md) | 简体中文

## 如何选择

- **灵巧手控制：**选择 C++ 或 Python 灵巧手 SDK；需要 ROS 话题和服务时，选择灵巧手 ROS 2 SDK。
- **机械臂控制：**选择机械臂 Python SDK 或机械臂 ROS 2 SDK。
- **遥操作：**数据手套到灵巧手的动作映射使用 `linkerhand-telop-ros2`；双臂输入设备的关节读取使用 `linkerhand-tele-arm`。
- **通信接入：**只需要底层通信、不需要设备控制接口时，选择 C++ 或 Python 通信库。
- **已有应用：**更换 SDK 前，先阅读旧版本项目说明。

以下维护分类依据截至 **2026-11-06** 的 SDK 目录维护计划，
不代表对应仓库已经归档。具体支持的型号、固件、适配器、平台及安装要求，以各项目文档为准。

## 正在维护的项目

### 通信库

- [**linkerbot-transport-cpp**](https://github.com/linker-bot/linkerbot-transport-cpp) — C++17 通信库，提供 CAN/CAN FD 后端、连接共享、帧路由和发送回执。当前源码还提供可选的串口与 Modbus RTU 模块，具体可用性取决于所选版本。设备协议与运动控制由设备 SDK 实现。
- [**linkerbot-transport**](https://github.com/linker-bot/linkerbot-transport) — Python 通信层，支持经典 CAN 和 CAN FD，提供接收路由、连接共享、发送结果和发送调度，不依赖 ROS 或具体设备型号。

### C++ SDK 与工具

- [**linkerbot-hand-cpp-sdk**](https://github.com/linker-bot/linkerbot-hand-cpp-sdk) — C++17 灵巧手 SDK，基于 `linkerbot-transport-cpp` 提供设备发现、关节控制、传感器读取和后台遥测。选用硬件前，请查阅型号能力与兼容性文档。
- [**linkerhand-tele-arm**](https://github.com/linker-bot/linkerhand-tele-arm) — 通过 Linux SocketCAN 读取双臂输入设备的 14 个关节，提供 C++17 核心库、命令行工具和 ROS 2 节点。该项目用于读取输入设备，不是机械臂运动控制 SDK。

### Python 与 ROS 2 SDK

- [**linkerbot-hand-python-sdk**](https://github.com/linker-bot/linkerbot-hand-python-sdk) — Python 灵巧手 SDK，通过共享的 Python 通信库连接设备、读取状态和控制灵巧手。请从源码安装与连接指南开始使用。
- [**linkerbot-hand-ros2-sdk**](https://github.com/linker-bot/linkerbot-hand-ros2-sdk) — 灵巧手 ROS 2 接入，包含类型化消息和服务、Lifecycle 驱动以及 O6 URDF 滑块 GUI。依赖灵巧手 Python SDK 和通信库，提供 Humble/Jazzy 环境配置说明。
- [**linkerbot-arm-python-sdk**](https://github.com/linker-bot/linkerbot-arm-python-sdk) — 面向 A7、A7lite、P7 和 H75 机械臂的 Python SDK，提供关节控制、状态反馈及正逆运动学。Pinocchio 与通信依赖要求见项目文档。
- [**linkerbot-arm-ros2-sdk**](https://github.com/linker-bot/linkerbot-arm-ros2-sdk) — 基于机械臂 Python SDK，通过 ROS 2 话题和服务控制左右 A7、A7 Lite 和 P7 机械臂。请先阅读启动指南：默认配置会在启动时使能机械臂并执行回零。
- [**linkerhand-telop-ros2**](https://github.com/linker-bot/linkerhand-telop-ros2) — 面向受支持数据手套与 LinkerHand 型号的 ROS 2 遥操作和动作重定向工具，包含手套适配、模型资源、配置和示例。构建后需保留文档规定的源码工作空间结构；文档所述版本不支持仅复制 `install/` 目录部署。

## 旧版本项目：即将结束维护

以下项目保留用于已有应用。新项目在硬件与功能受支持的前提下，应优先选择正在维护的项目。
本目录未指定停止维护日期。下文提到的新项目仅作为迁移评估入口，不表示可以直接替换，也不保证覆盖旧型号。

- [**linkerhand-cpp-sdk**](https://github.com/linker-bot/linkerhand-cpp-sdk) — 旧版预编译 C++ 灵巧手 SDK，包含公开头文件、预编译库、示例和工具。其 README 仍说明会为新 SDK 尚未覆盖的设备提供兼容维护。迁移至 `linkerbot-hand-cpp-sdk` 前需逐型号核对。
- [**linkerbot-python-sdk**](https://github.com/linker-bot/linkerbot-python-sdk) — 较早的 Python 综合 SDK，包含灵巧手和机械臂功能。新接入可评估拆分后的灵巧手 Python SDK、机械臂 Python SDK 与通信库。
- [**linkerhand-python-sdk**](https://github.com/linker-bot/linkerhand-python-sdk) — 较早的 Python 灵巧手 SDK，提供 CAN/Modbus 配置与控制示例。可评估 `linkerbot-hand-python-sdk`，先确认设备与协议支持情况。
- [**linkerhand-ros2-sdk**](https://github.com/linker-bot/linkerhand-ros2-sdk) — 较早的 ROS 2 灵巧手驱动，包含控制示例、GUI 工具与触觉可视化。可评估 `linkerbot-hand-ros2-sdk`，核对消息、启动配置和型号差异。
- [**linkerhand-ros-sdk**](https://github.com/linker-bot/linkerhand-ros-sdk) — ROS 1 灵巧手驱动及功能示例。改用 `linkerbot-hand-ros2-sdk` 时，还需要完成应用从 ROS 1 到 ROS 2 的迁移。
- [**linkerhand-l30-sdk**](https://github.com/linker-bot/linkerhand-l30-sdk) — L30 专用 ROS 2 驱动，提供 CAN FD 通信、GUI 控制和可选触觉数据。迁移前需核对正在维护的灵巧手 SDK 对 L30 协议与功能的覆盖情况。
- [**linkerhand-o20-ros2**](https://github.com/linker-bot/linkerhand-o20-ros2) — O20 专用 ROS 2 驱动与 GUI 示例，使用 CAN FD 通信。需单独确认 O20 支持情况，不能由 O30 支持情况推定兼容。
- [**linkerhand-l20d-ros2**](https://github.com/linker-bot/linkerhand-l20d-ros2) — L20D 专用 ROS 2 驱动，包含 GUI、手部状态话题与触觉数据。需明确核对 L20D 支持情况，不能仅凭 L20 等相似型号名称判断兼容。
- [**linkerhand-cpp-ros2**](https://github.com/linker-bot/linkerhand-cpp-ros2) — 旧版 C++ 灵巧手 SDK 的 ROS 2 封装，包含启动配置与 GUI 工具。替换前需评估正在维护的灵巧手 ROS 2 SDK 的接口与型号覆盖情况。
- **linkerhand-ros-teleop** — 本目录提供的旧版遥操作项目入口。[原仓库地址](https://github.com/linker-bot/linkerhand-ros-teleop)在 2026-11-06 检查时返回 404，无法核实内容与兼容性。当前 ROS 2 遥操作需求可评估 `linkerhand-telop-ros2`。

## 文档与许可证

安装步骤、API、硬件限制和发布信息以各项目仓库为准。本目录不分发 SDK 或驱动。
本仓库使用 [Apache License 2.0](LICENSE)；所链接项目使用各自的许可证。
