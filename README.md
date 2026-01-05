
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

## Prerequisites & Building on macOS (Apple Silicon)

### ✅ Tested Configuration

Successfully built and tested on:
- **Platform:** macOS (Darwin) ARM64
- **Hardware:** M5 MacBook Pro
- **Compiler:** Apple Clang 17.0.0
- **CMake:** 3.10+
- **OpenCV:** 4.13.0
- **Eigen:** 5.0.1
- **Boost:** 1.90.0
- **OpenSSL:** 3.6.0
- **Pangolin:** Installed (built from source)

### 1. Install Homebrew (if not already installed)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. Install Required Dependencies

```bash
# Essential build tools
brew install cmake pkg-config

# Core dependencies
brew install eigen boost opencv

# Graphics dependencies (for viewer support)
brew install glew

# OpenSSL (required for cryptographic functions)
brew install openssl

# Optional: Pangolin (for visualization)
# Note: May need to build from source on macOS
brew install pangolin  # or build from https://github.com/stevenlovegrove/Pangolin
```

### 3. Clone and Build

```bash
# Clone the repository
git clone https://github.com/Dmitrii173173/ORB_SLAM3_macOS_arm64.git
cd ORB_SLAM3_macOS_arm64

# Build everything (libraries + examples)
chmod +x build.sh
./build.sh
```

The build script will:
1. Build third-party libraries (DBoW2, g2o, Sophus)
2. Uncompress the vocabulary
3. Build the main ORB-SLAM3 library (`lib/libORB_SLAM3.dylib`)
4. Build example programs

### 🔧 Key Modifications for Apple Silicon

This fork includes the following platform-specific adaptations:

1. **Compiler Flags:** `-march=native` → `-mcpu=apple-m1` for Apple Silicon
2. **Library Extensions:** `.so` → `.dylib` for macOS
3. **C++ Standard:** Updated to C++14 (required for Eigen 5.x, backward compatible with C++11)
4. **Header Files:**
   - `stdint-gcc.h` → `cstdint`
   - `tr1/unordered_map` → `unordered_map` (C++11 standard)
   - `tr1/memory` → `memory` (C++11 standard)
5. **OpenSSL:** Added proper detection and linking
6. **Time Measurement:** `std::chrono::monotonic_clock` → `steady_clock` (macOS compatible)
7. **Eigen:** Configured for Eigen 5.0.1 from Homebrew

### 🚀 Running Examples

After successful build, you can run the examples:

#### Monocular Examples

```bash
# TUM Dataset
./Examples/Monocular/mono_tum \
    Vocabulary/ORBvoc.txt \
    Examples/Monocular/TUM1.yaml \
    PATH_TO_SEQUENCE_FOLDER

# KITTI Dataset
./Examples/Monocular/mono_kitti \
    Vocabulary/ORBvoc.txt \
    Examples/Monocular/KITTI00-02.yaml \
    PATH_TO_SEQUENCE_FOLDER

# EuRoC Dataset
./Examples/Monocular/mono_euroc \
    Vocabulary/ORBvoc.txt \
    Examples/Monocular/EuRoC.yaml \
    PATH_TO_SEQUENCE_FOLDER \
    Examples/Monocular/EuRoC_TimeStamps/SEQUENCE.txt
```

#### Stereo Examples

```bash
# KITTI Dataset
./Examples/Stereo/stereo_kitti \
    Vocabulary/ORBvoc.txt \
    Examples/Stereo/KITTI00-02.yaml \
    PATH_TO_SEQUENCE_FOLDER

# EuRoC Dataset
./Examples/Stereo/stereo_euroc \
    Vocabulary/ORBvoc.txt \
    Examples/Stereo/EuRoC.yaml \
    PATH_TO_SEQUENCE_FOLDER \
    Examples/Stereo/EuRoC_TimeStamps/SEQUENCE.txt
```

#### RGB-D Examples

```bash
# TUM Dataset
./Examples/RGB-D/rgbd_tum \
    Vocabulary/ORBvoc.txt \
    Examples/RGB-D/TUM1.yaml \
    PATH_TO_SEQUENCE_FOLDER \
    ASSOCIATIONS_FILE
```

#### Monocular-Inertial Examples

```bash
# EuRoC Dataset
./Examples/Monocular-Inertial/mono_inertial_euroc \
    Vocabulary/ORBvoc.txt \
    Examples/Monocular-Inertial/EuRoC.yaml \
    PATH_TO_SEQUENCE_FOLDER \
    Examples/Monocular-Inertial/EuRoC_TimeStamps/SEQUENCE.txt \
    dataset-SEQUENCE_stereorectified.txt
```

#### Stereo-Inertial Examples

```bash
# EuRoC Dataset
./Examples/Stereo-Inertial/stereo_inertial_euroc \
    Vocabulary/ORBvoc.txt \
    Examples/Stereo-Inertial/EuRoC.yaml \
    PATH_TO_SEQUENCE_FOLDER \
    Examples/Stereo-Inertial/EuRoC_TimeStamps/SEQUENCE.txt \
    dataset-SEQUENCE_stereorectified.txt
```

**Note:** Replace `PATH_TO_SEQUENCE_FOLDER` and `SEQUENCE` with actual dataset paths and sequence names.

---

# ORB_SLAM3_macOS_arm64
