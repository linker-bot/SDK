# Evaluating a legacy SDK migration

English | [简体中文](MIGRATION.zh-CN.md) | [Project directory](README.md)

The directory distinguishes maintained projects from legacy projects whose maintenance
is ending. It does not specify a retirement date or promise API compatibility between generations.

## Select a candidate

- Legacy C++ hand applications: evaluate [linkerbot-hand-cpp-sdk](https://github.com/linker-bot/linkerbot-hand-cpp-sdk). Keep the legacy SDK where required models or communication paths are not covered.
- Legacy Python hand applications: evaluate [linkerbot-hand-python-sdk](https://github.com/linker-bot/linkerbot-hand-python-sdk).
- Applications using the combined `linkerbot-python-sdk`: evaluate the separate [hand](https://github.com/linker-bot/linkerbot-hand-python-sdk), [arm](https://github.com/linker-bot/linkerbot-arm-python-sdk), and [transport](https://github.com/linker-bot/linkerbot-transport) projects according to the components actually used.
- Legacy hand ROS applications, including model-specific and C++ wrappers: evaluate [linkerbot-hand-ros2-sdk](https://github.com/linker-bot/linkerbot-hand-ros2-sdk). ROS 1 applications also require a ROS 2 migration; a Python-based ROS 2 driver is not a replacement C++ library.
- Legacy teleoperation applications: evaluate [linkerhand-telop-ros2](https://github.com/linker-bot/linkerhand-telop-ros2). The legacy [linkerhand-ros-teleop](https://github.com/linker-bot/linkerhand-ros-teleop) repository documents ROS 1/ROS 2 glove retargeting; no equivalence is asserted.

Legacy C++ interactive tools now live in [linkerbot-hand-tools](https://github.com/linker-bot/linkerbot-hand-tools). The legacy SDK CMake package is `linkerhand-legacy-cpp-sdk`, with target `LinkerHand::linkerhand_legacy_cpp_sdk`; update package lookups and explicit installation paths when adopting the renamed package.

## Check compatibility before switching

1. Record the current repository revision, configuration, device model, firmware, adapter, and driver. Keep a reproducible copy of the working deployment.
2. Confirm the exact model and protocol in the candidate's capability documentation. Check O20 and L20D explicitly; similar model names do not establish compatibility. The legacy C++ SDK still documents compatibility maintenance for models outside the newer SDK's scope.
3. Compare API and ROS interfaces: imports, package names, topics, services, message types, units, joint order, ranges, and startup behavior. Review initialization side effects before connecting hardware.
4. Follow the candidate's dependency instructions. Use its documented transport revision or version requirements and matching ROS/Python environment; do not combine installation commands from different generations.
5. Build and run the project's offline checks first. Then validate discovery and read-only feedback with the actual hardware before testing motion under the project's operating instructions. Offline tests do not validate motion or stopping behavior.
6. Switch only after application requirements are verified, retaining the previous deployment for rollback. If a required feature is missing, report it to the candidate project with the model, firmware, software revisions, and reproduction details.

## Maintain this directory

Update the English and Chinese directories together. For each entry, check the repository
URL, project purpose, and source documentation. Separate planned maintenance changes from
actual archival or retirement. Do not infer replacement compatibility from naming or activity.
When a repository is unavailable, retain its identity and state what could not be verified.

Check relative links and section navigation after editing. This repository contains no SDK
implementation, so software and hardware checks belong in the linked projects.
