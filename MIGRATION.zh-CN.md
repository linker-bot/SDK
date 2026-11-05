# 旧版 SDK 迁移评估

[English](MIGRATION.md) | 简体中文 | [项目目录](README.zh-CN.md)

项目目录区分正在维护的项目与即将结束维护的旧项目，未指定停止维护日期，也不承诺不同代 SDK 的 API 兼容。

## 选择评估对象

- 旧版 C++ 灵巧手应用：评估 [linkerbot-hand-cpp-sdk](https://github.com/linker-bot/linkerbot-hand-cpp-sdk)。所需型号或通信方式未覆盖时，保留旧版 SDK。
- 旧版 Python 灵巧手应用：评估 [linkerbot-hand-python-sdk](https://github.com/linker-bot/linkerbot-hand-python-sdk)。
- 使用综合包 `linkerbot-python-sdk` 的应用：根据实际使用的组件，分别评估[灵巧手](https://github.com/linker-bot/linkerbot-hand-python-sdk)、[机械臂](https://github.com/linker-bot/linkerbot-arm-python-sdk)和[通信库](https://github.com/linker-bot/linkerbot-transport)。
- 旧版灵巧手 ROS 应用，包括专用型号驱动和 C++ 封装：评估 [linkerbot-hand-ros2-sdk](https://github.com/linker-bot/linkerbot-hand-ros2-sdk)。ROS 1 应用还需迁移至 ROS 2；基于 Python 的 ROS 2 驱动不能作为 C++ 库直接替换。
- 旧版遥操作应用：评估 [linkerhand-telop-ros2](https://github.com/linker-bot/linkerhand-telop-ros2)。旧版 [linkerhand-ros-teleop](https://github.com/linker-bot/linkerhand-ros-teleop) 仓库提供 ROS 1/ROS 2 手套动作重定向说明，不据此认定功能等价。

旧版 C++ 交互工具已迁移至 [linkerbot-hand-tools](https://github.com/linker-bot/linkerbot-hand-tools)。旧版 SDK 的 CMake 包名为 `linkerhand-legacy-cpp-sdk`，目标为 `LinkerHand::linkerhand_legacy_cpp_sdk`；采用更名后的包时，需更新包查找和显式安装路径。

## 切换前核对

1. 记录现有仓库提交、配置、设备型号、固件、适配器和驱动，保留可复现的工作环境。
2. 在候选项目的能力文档中确认具体型号与协议。O20、L20D 等需单独核对，相似命名不代表兼容。旧版 C++ SDK 仍说明会为新 SDK 尚未覆盖的型号提供兼容维护。
3. 对比 API 与 ROS 接口，包括导入路径、包名、话题、服务、消息类型、单位、关节顺序、取值范围和启动行为。连接硬件前先检查初始化可能触发的操作。
4. 按候选项目的依赖说明安装，使用其规定的通信库提交或版本要求，以及匹配的 ROS/Python 环境，不要混用不同代项目的安装命令。
5. 先构建并运行项目的离线检查，再使用实际硬件验证设备发现和只读反馈，最后按照项目操作说明测试运动。离线测试不能验证实际运动或停止行为。
6. 应用需求验证通过后再切换，保留原部署用于回退。所需功能缺失时，向候选项目反馈具体型号、固件、软件提交与复现信息。

## 维护本目录

同步更新中英文目录，逐项核对仓库地址、项目用途与源文档。区分维护计划调整与实际归档、停止维护状态，
不要根据项目命名或活跃度推定替代关系。仓库不可访问时，保留项目名称并说明无法核实的内容。

编辑后检查相对链接与章节导航。本仓库不包含 SDK 实现，软件与硬件验证应在对应项目中完成。
