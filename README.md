# OpenCvSharp 4 Mini Runtime [![QQ](https://img.shields.io/badge/QQ_Group-579060605-52B6EF?style=social&logo=tencent-qq&logoColor=000&logoWidth=20)](https://jq.qq.com/?_wv=1027&k=K4fBqpyQ)
[![Build-OpenCV](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/opencv.yml/badge.svg)](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/opencv.yml) [![Build-OpenCvSharp](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/opencvsharp.yml/badge.svg)](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/opencvsharp.yml) [![Test-OpenCvSharp](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/test-opencvsharp.yml/badge.svg)](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/test-opencvsharp.yml) [![Make-NuGet](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/make-nuget.yml/badge.svg)](https://github.com/sdcb/opencvsharp-mini-runtime/actions/workflows/make-nuget.yml)

Mini runtime that suitable for model inference in server, only `core`, `imgproc`, `imgcodec` modules was built.

Packages are all built & integration-tested by a fully automated CI/CD pipeline on GitHub, CICD code fully open source.

### 📦  OpenCvSharp Mini-Runtime Matrix

| OS            | Package Id                                        | NuGet                                                                                                                                                                              | Compiler        | Mini-ABI          |
| ------------- | ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | ----------------- |
| Windows       | Sdcb.OpenCvSharp4.mini.runtime.win-x64            | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.win-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.win-x64)                       | MSVC            | win-x64           |
|               | Sdcb.OpenCvSharp4.mini.runtime.win-x86            | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.win-x86.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.win-x86)                       | MSVC            | win-x86           |
|               | Sdcb.OpenCvSharp4.mini.runtime.win-arm64          | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.win-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.win-arm64)                   | MSVC            | win-arm64         |
| Linux (glibc) | Sdcb.OpenCvSharp4.mini.runtime.centos.7-x64       | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.centos.7-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.centos.7-x64)             | GCC 4.8.5       | glibc 2.17+       |
|               | Sdcb.OpenCvSharp4.mini.runtime.centos.7-arm64     | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.centos.7-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.centos.7-arm64)         | GCC 4.8.5       | glibc 2.17+       |
|               | Sdcb.OpenCvSharp4.mini.runtime.linux-x64          | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.linux-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.linux-x64)                   | GCC 8.5.0       | glibc 2.28+       |
|               | Sdcb.OpenCvSharp4.mini.runtime.linux-arm64        | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.linux-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.linux-arm64)               | GCC 8.5.0       | glibc 2.28+       |
|               | Sdcb.OpenCvSharp4.mini.runtime.ubuntu.22.04-x64   | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.ubuntu.22.04-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.ubuntu.22.04-x64)     | GCC 11.2.0      | glibc 2.35        |
|               | Sdcb.OpenCvSharp4.mini.runtime.ubuntu.22.04-arm64 | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.ubuntu.22.04-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.ubuntu.22.04-arm64) | GCC 11.2.0      | glibc 2.35        |
| Linux (musl)  | Sdcb.OpenCvSharp4.mini.runtime.linux-musl-x64     | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.linux-musl-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.linux-musl-x64)         | GCC 13.2.0      | musl 1.2 (static) |
|               | Sdcb.OpenCvSharp4.mini.runtime.linux-musl-arm64   | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.linux-musl-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.linux-musl-arm64)     | GCC 13.2.0      | musl 1.2 (static) |
| macOS         | Sdcb.OpenCvSharp4.mini.runtime.osx-x64            | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.osx-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.osx-x64)                       | Xcode 15        | macOS 10.15+      |
|               | Sdcb.OpenCvSharp4.mini.runtime.osx-arm64          | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.osx-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.osx-arm64)                   | Xcode 15        | macOS 11+         |
| Android       | Sdcb.OpenCvSharp4.mini.runtime.android-x64        | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.android-x64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.android-x64)               | Clang (NDK r27) | API 24+, static   |
|               | Sdcb.OpenCvSharp4.mini.runtime.android-arm64      | [![NuGet](https://img.shields.io/nuget/v/Sdcb.OpenCvSharp4.mini.runtime.android-arm64.svg)](https://www.nuget.org/packages/Sdcb.OpenCvSharp4.mini.runtime.android-arm64)           | Clang (NDK r27) | API 24+, static   |

---

## 🔍 End-to-end automated tests in
* 20 native OS installations
* 79 Docker containers
* Android-x64 emulator

Assurance: every package runs reliably on its target platform.

---

## 🖥️ Platform Quick-Start

### Windows
• Use **win-x64** (most PCs) or **win-x86** (legacy).  
• Tested on Windows Server 2022 & 2025; older versions should work thanks to Windows’ strong ABI compatibility.  
• **win-arm64** is now available and verified for Windows on ARM devices.

### Linux (glibc)
Three flavours, each shipping x64 & arm64 artifacts and **dynamically** linking `libstdc++.so.6` + `libgcc_s.so.1`.

1. **centos.7** – built with GCC 4.8.5 (patched); runs on glibc 2.17+  
   Ideal for CentOS 7 / RHEL 7, Debian 8+, Ubuntu 14.04+.

2. **linux** – built with GCC 8.5.0; no source patches.  
   Runs on glibc 2.28+ (RHEL 8+, Debian 10+, Ubuntu 20.04+, openEuler 20.03-lts, Deepin, …).  
   👉 Recommended default for most users.

3. **ubuntu.22.04** – built with GCC 11.2.0.  
   Works on Ubuntu 22.04+, Debian 11+, RHEL 9+. Slightly narrower compatibility; may be retired if adoption is low.

> Before 4.11.0, the “linux” package was built on Ubuntu 22.04, so 4.11.0 greatly **improves compatibility**.

### Linux (musl)
Packages **linux-musl-x64 / arm64** are built on Alpine 3.22 and **statically** link `libstdc++` & `libgcc`.  
Confirmed to run on Alpine 3.12 (musl 1.1.24) — even routers running OpenWrt!

### Android
**android-x64 / arm64** compiled with Android NDK r27, API 24.  
`libstdc++` is statically linked, so drop-in ready for any device running Android 7.0+.

### macOS
• **osx-x64** for Intel Macs.  
• **osx-arm64** for Apple Silicon (M1 → M4).  
Both cross-tested on macOS 14 & 15.

---

## 📦 Packages No Longer Published
The following SKUs are now redundant; switch to the recommended replacements:

| Deprecated                | Use Instead                               |
| ------------------------- | ----------------------------------------- |
| ubuntu.24.04-x64/arm64    | linux-x64/arm64 or ubuntu.22.04-x64/arm64 |
| win11-x64                 | win-x64                                   |
| osx.15-arm64              | osx-arm64                                 |
| rhel9-x64/arm64 (planned) | linux-x64/arm64                           |

---

## ⭐ How You Can Help
If these runtimes make your life easier, please…

1. **Star** the repo: https://github.com/sdcb/opencvsharp-mini-runtime  
2. Consider a small **donation** – let me know your special needs and I’ll try to publish a build that fits.

Thanks for using OpenCvSharp mini-runtime and happy hacking!  
— @Sdcb