# OpenCvSharp 4 Mini Runtime [![QQ](https://img.shields.io/badge/QQ_Group-579060605-52B6EF?style=social&logo=tencent-qq&logoColor=000&logoWidth=20)](https://jq.qq.com/?_wv=1027&k=K4fBqpyQ)
[![Build-OpenCV](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/opencv.yml/badge.svg)](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/opencv.yml) [![Build-OpenCvSharp](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/opencvsharp.yml/badge.svg)](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/opencvsharp.yml) [![Test-OpenCvSharp](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/test-opencvsharp.yml/badge.svg)](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/test-opencvsharp.yml) [![Make-NuGet](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/make-nuget.yml/badge.svg)](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/make-nuget.yml)

[English](README.md) | **简体中文**

OpenCvSharp 4 Mini Runtime 是面向服务端模型推理场景的轻量运行时包。当前维护的包会构建 `core`、`imgproc`、`imgcodecs`，并且从 `4.13.0.45` 开始加入 `dnn` 模块。

`osx-arm64` 是唯一例外：它仍然包含 `core`、`imgproc`、`imgcodecs`，但暂不包含 `dnn`。原因是 GitHub Actions 的 macOS arm64 runner 在 OpenCV DNN 构建阶段会反复卡住。

所有包都由 GitHub 上完全自动化、公开的 CI/CD 流程构建并做集成测试。

### 📦 当前维护的 OpenCvSharp Mini-Runtime 矩阵

| OS            | Package Id                                      | NuGet                                                                                                                                                                      | Compiler        | Mini-ABI        | Modules                         |
| ------------- | ----------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | --------------- | ------------------------------- |
| Windows       | Sdcb.OpenCvSharp4.mini.runtime.win-x64          | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.win-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.win-x64)               | MSVC 17         | win-x64         | core, imgproc, imgcodecs, dnn   |
|               | Sdcb.OpenCvSharp4.mini.runtime.win-x86          | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.win-x86.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.win-x86)               | MSVC 17         | win-x86         | core, imgproc, imgcodecs, dnn   |
|               | Sdcb.OpenCvSharp4.mini.runtime.win-arm64        | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.win-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.win-arm64)           | MSVC 17         | win-arm64       | core, imgproc, imgcodecs, dnn   |
| Linux (glibc) | Sdcb.OpenCvSharp4.mini.runtime.linux-x64        | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.linux-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.linux-x64)           | GCC 8.5.0       | glibc 2.28+     | core, imgproc, imgcodecs, dnn   |
|               | Sdcb.OpenCvSharp4.mini.runtime.linux-arm64      | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.linux-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.linux-arm64)       | GCC 8.5.0       | glibc 2.28+     | core, imgproc, imgcodecs, dnn   |
| Linux (musl)  | Sdcb.OpenCvSharp4.mini.runtime.linux-musl-x64   | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.linux-musl-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.linux-musl-x64) | GCC 14.2.0      | musl 1.2 static | core, imgproc, imgcodecs, dnn   |
|               | Sdcb.OpenCvSharp4.mini.runtime.linux-musl-arm64 | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.linux-musl-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.linux-musl-arm64) | GCC 14.2.0   | musl 1.2 static | core, imgproc, imgcodecs, dnn   |
| macOS         | Sdcb.OpenCvSharp4.mini.runtime.osx-x64          | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.osx-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.osx-x64)               | Xcode 16        | macOS 10.15+    | core, imgproc, imgcodecs, dnn   |
|               | Sdcb.OpenCvSharp4.mini.runtime.osx-arm64        | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.osx-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.osx-arm64)           | Xcode 16        | macOS 11+       | core, imgproc, imgcodecs        |
| Android       | Sdcb.OpenCvSharp4.mini.runtime.android-x64      | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.android-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.android-x64)       | Clang (NDK r27) | API 24+, static | core, imgproc, imgcodecs, dnn   |
|               | Sdcb.OpenCvSharp4.mini.runtime.android-arm64    | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.android-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.android-arm64)   | Clang (NDK r27) | API 24+, static | core, imgproc, imgcodecs, dnn   |

### 🧊 已过期的 Runtime 矩阵

这些包仍然保留在 NuGet 上以兼容既有用户，但当前流水线不再主动构建或验证它们。

| OS / Baseline  | Package Id Prefix                                        | 历史用途                                  | 推荐替代                                  |
| -------------- | -------------------------------------------------------- | ----------------------------------------- | ----------------------------------------- |
| CentOS 7       | Sdcb.OpenCvSharp4.mini.runtime.centos.7-*                | glibc 2.17 时代系统                       | linux-x64 / linux-arm64                   |
| Ubuntu 22.04   | Sdcb.OpenCvSharp4.mini.runtime.ubuntu.22.04-*            | glibc 2.35 特定构建                       | linux-x64 / linux-arm64                   |
| Ubuntu 24.04   | Sdcb.OpenCvSharp4.mini.runtime.ubuntu.24.04-*            | 实验性较新 glibc 构建                     | linux-x64 / linux-arm64                   |
| Windows 11     | Sdcb.OpenCvSharp4.mini.runtime.win11-x64                 | Windows 11 专用 runner label 实验         | win-x64                                   |
| macOS 15       | Sdcb.OpenCvSharp4.mini.runtime.osx.15-arm64              | macOS 15 专用 runner label 实验           | osx-arm64                                 |
| RHEL 9         | Sdcb.OpenCvSharp4.mini.runtime.rhel9-*                   | 曾计划单独维护，但当前不再单独维护        | linux-x64 / linux-arm64                   |

---

## 🔍 端到端自动化测试

* 11 个包构建/链接 smoke test
* 11 个原生宿主机 runtime test
* 36 个 Docker 容器兼容性测试
* Android x64 模拟器 runtime test

目标是保证每个包都能在目标平台上可靠运行。

---

## 🖥️ 平台快速选择

### Windows

• 普通 PC 使用 **win-x64**，老旧 32 位进程使用 **win-x86**。  
• 已在 Windows Server 2022 与 2025 上测试；得益于 Windows ABI 兼容性，较老版本通常也可以工作。  
• **win-arm64** 已可用于 Windows on ARM 设备，并已验证。

### Linux (glibc)

当前维护的 **linux-x64 / arm64** 包基于 RHEL 8 构建，并且 **动态链接** `libstdc++.so.6` 与 `libgcc_s.so.1`。

它们可运行在 glibc 2.28+ 的发行版上，包括 RHEL 8+、Debian 10+、Ubuntu 20.04+、openEuler 20.03-lts、Deepin 以及更新的系统。

### Linux (musl)

**linux-musl-x64 / arm64** 包基于 Alpine 3.22 构建，并且 **静态链接** `libstdc++` 与 `libgcc`。  
已确认可运行在 Alpine 3.12 (musl 1.1.24) 上，也适合 OpenWrt 等更小型的 musl 环境。

### Android

**android-x64 / arm64** 使用 Android NDK r27、API 24 编译。  
`libstdc++` 静态链接，可直接用于 Android 7.0+ 设备。

### macOS

• **osx-x64** 用于 Intel Mac。  
• **osx-arm64** 用于 Apple Silicon (M1 -> M4)。  
两者都在 macOS 15 runner 上测试。`osx-arm64` 当前不包含 `dnn`，因为 OpenCV DNN 在 GitHub Actions macOS arm64 基础设施上会反复卡住。

---

## ⭐ 如何支持

如果这些 runtime 对你有帮助，可以：

1. **Star** 这个仓库：https://github.com/sdcb/opencvsharp-mini-runtime
2. 考虑小额 **捐赠**。如果你有特殊平台需求，也可以告诉我，我会尽量发布适配构建。

感谢使用 OpenCvSharp mini-runtime。  
— @Sdcb
