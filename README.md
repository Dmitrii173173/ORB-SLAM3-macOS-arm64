![orb_slam_pi](https://github.com/user-attachments/assets/a8a38676-426f-47ed-b7e8-c148267189f2)

# ORB-SLAM3 macOS (Apple Silicon, arm64)

![macOS](https://img.shields.io/badge/platform-macOS%20ARM64-blue)
![License](https://img.shields.io/badge/license-GPLv3-green)
![Status](https://img.shields.io/badge/status-community--maintained-yellow)

⚠️ **Important Notice**

This repository is a **community-maintained macOS Apple Silicon (arm64) port**
of the original **ORB-SLAM3** project:

https://github.com/UZ-SLAMLab/ORB_SLAM3

The original ORB-SLAM3 library was designed and extensively tested on
**Linux (x86_64)**.  
This repository focuses **exclusively on build compatibility and usability
on macOS Apple Silicon**, without introducing new SLAM methods or modifying
the underlying algorithms.

➡️ **All algorithmic, scientific, and research credit belongs to the original authors.**

---

## About

ORB-SLAM3 is a state-of-the-art open-source system for **visual, visual-inertial,
and multi-map SLAM**, supporting:

- monocular cameras  
- stereo cameras  
- RGB-D cameras  
- visual–inertial configurations  

It is widely used in academic research and experimental robotics.

This repository adapts the original ORB-SLAM3 codebase for execution on
**Apple Silicon–based macOS systems (arm64)**, enabling researchers and
developers to work with ORB-SLAM3 natively on modern Mac hardware.

---

## Scope and Intent

This repository exists **solely to improve buildability and usability**
of ORB-SLAM3 on macOS Apple Silicon.

### This repository **DOES**:
- provide macOS (arm64) build support,
- update legacy build configuration where required,
- document macOS-specific dependencies and limitations,
- preserve original algorithmic behavior.

### This repository **DOES NOT**:
- introduce new SLAM algorithms,
- change mathematical models or optimization logic,
- claim official support on behalf of the original authors,
- replace or compete with the upstream ORB-SLAM3 project.

---

## Relationship to Upstream ORB-SLAM3

This project is a **derivative work** of ORB-SLAM3 under the GPLv3 license.

Upstream ORB-SLAM3 remains the authoritative source for:
- algorithmic development,
- research contributions,
- official releases,
- benchmarking and evaluation.

This repository focuses **only** on platform compatibility for macOS
Apple Silicon and does not track upstream feature development beyond what
is required for successful builds.

---

## macOS (Apple Silicon) Notes

- macOS is **not an officially supported platform** by the original ORB-SLAM3 authors.
- Viewer support via Pangolin is **optional** and may be limited due to
  OpenGL constraints on macOS.
- The primary focus is **headless execution and core SLAM functionality**.
- Performance characteristics may differ from Linux x86_64 builds.

---

## Intended Audience

This repository is intended for:
- researchers and students working on macOS Apple Silicon,
- developers prototyping SLAM systems on Mac hardware,
- academic experimentation and learning.

This repository is **not intended** for:
- production robotics deployments,
- real-time embedded systems,
- official performance benchmarking.

---

## Tested Configuration

Successfully built and tested on:

- **Platform:** macOS (Darwin) ARM64  
- **Hardware:** Apple Silicon (M-series)  
- **Compiler:** Apple Clang 17.0.0  
- **CMake:** 3.10+  
- **OpenCV:** 4.13.0  
- **Eigen:** 5.0.1  
- **Boost:** 1.90.0  
- **OpenSSL:** 3.6.0  
- **Pangolin:** Built from source  

---

## Building on macOS (Apple Silicon)

### 1. Install

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
![orb_slam_pi](https://github.com/user-attachments/assets/9c9d9d9a-c990-4cf4-962e-7f2d161cbb68)


brew update
brew install eigen boost opencv
brew install glew
brew install openssl
https://github.com/stevenlovegrove/Pangolin

chmod +x build.sh
./build.sh






 ### 2. For kitti

## ▶️ Running ORB-SLAM3 with KITTI Dataset (macOS)

### Run command

```bash
./Examples/Stereo/stereo_kitti_macos \
Vocabulary/ORBvoc.txt \
Examples/Stereo/KITTI04-12.yaml \
dataset/dataset/sequences/00
```

### Parameters explanation

1. `./Examples/Stereo/stereo_kitti_macos` — executable binary
2. `Vocabulary/ORBvoc.txt` — ORB feature descriptor vocabulary
3. `Examples/Stereo/KITTI04-12.yaml` — camera configuration file for the KITTI dataset
4. `dataset/dataset/sequences/00` — path to KITTI sequence **00**

---

### Running other KITTI sequences

```bash
# Sequence 01
./Examples/Stereo/stereo_kitti_macos \
Vocabulary/ORBvoc.txt \
Examples/Stereo/KITTI04-12.yaml \
dataset/dataset/sequences/01

# Sequence 02
./Examples/Stereo/stereo_kitti_macos \
Vocabulary/ORBvoc.txt \
Examples/Stereo/KITTI04-12.yaml \
dataset/dataset/sequences/02
```

---

### 🖥 Pangolin Viewer Controls

* **ESC** or close window — exit
* **Mouse drag** — rotate camera
* **Mouse scroll** — zoom in / out
* **Right mouse button** — pan view

---

### 📄 Output

After execution, trajectory files will be generated:

* `CameraTrajectory.txt` — estimated camera trajectory in **KITTI format**



## 📁 Project Directory Structure

```text
ORB_SLAM3_macOS_arm64/
├── Examples/
│   ├── Stereo/
│   │   ├── stereo_kitti
│   │   ├── stereo_euroc
│   │   ├── KITTI04-12.yaml
│   │   └── EuRoC.yaml
│
├── Vocabulary/
│   └── ORBvoc.txt
│
├── dataset/
│   └── dataset/
│       └── sequences/
│           └── 00/
│               ├── image_0/        # Left camera images
│               ├── image_1/        # Right camera images
│               └── times.txt       # Timestamps (seconds)
```

### Notes

* `image_0/` and `image_1/` contain grayscale stereo image pairs from the KITTI dataset
* `times.txt` provides per-frame timestamps required by ORB-SLAM3
* Camera intrinsics and stereo calibration are defined in `KITTI04-12.yaml`
* ORB vocabulary is loaded from `Vocabulary/ORBvoc.txt`






