
![orb_slam_pi](https://github.com/user-attachments/assets/4fbfd026-f891-47bf-985c-d9220b01510e)

# ORB-SLAM3_macOS_arm64

⚠️ **Important Notice**

This repository is a **community-maintained fork** of the original
[ORB-SLAM3](https://github.com/UZ-SLAMLab/ORB_SLAM3) project,
adapted specifically for **macOS on Apple Silicon (arm64)**.

The original ORB-SLAM3 library was designed and extensively tested on
Linux (x86_64). This fork focuses exclusively on **platform compatibility**
and **build support for macOS**, without introducing new SLAM methods or
modifying the core algorithms.

➡️ **All algorithmic and scientific credit belongs to the original authors.**

---

## About This Fork

ORB-SLAM3 is a state-of-the-art open-source library for **visual,
visual-inertial, and multi-map SLAM**, supporting monocular, stereo, and
RGB-D camera configurations.

**ORB-SLAM3_macOS_arm64** builds upon the original implementation and adapts
it for execution on **Apple Silicon–based macOS systems (arm64)**.

The primary goals of this fork are:

- build compatibility with macOS (arm64),
- support for modern CMake toolchains,
- stable headless execution (viewer optional or disabled by default),
- minimal, transparent, and well-documented platform-specific changes.

This fork does **not** aim to:
- introduce new SLAM algorithms,
- change the mathematical foundations of ORB-SLAM3,
- provide official macOS support on behalf of the original authors.

---

## macOS (Apple Silicon) Notes

- macOS is **not an officially supported platform** by the original ORB-SLAM3 authors.
- The Pangolin-based viewer is **optional or disabled** in this fork due to
  limited OpenGL support on macOS.
- The focus is on **core SLAM functionality**, not GUI or visualization.
- Tested on Apple Silicon devices (M-series, arm64).

---

## Scope of This Fork

This repository exists solely to improve **buildability and usability**
of ORB-SLAM3 on macOS systems using Apple Silicon.

All changes are limited to:
- build system adjustments,
- dependency compatibility fixes,
- platform-specific conditionals.

Algorithmic behavior remains consistent with the upstream project.

---

## Prerequisites

⚠️ **macOS users**

The instructions below describe the **original Linux-based setup** provided
by the ORB-SLAM3 authors.

macOS-specific build instructions, dependencies, and known limitations are
documented separately in `BUILD_MACOS.md`.

Please refer to that document before attempting to build this fork on macOS.

---

