<div align = center>

<img src="https://github.com/co2kernel/.github/raw/refs/heads/main/profile/logo.png" width="462" height="146" style="display: block; margin: 0 auto;" alt="CO₂Kernel">

---
Customized kernel built for Hedwig/Xueying (OnePlus Open)

[![简体中文][readme-cn-badge]][readme-cn-url]
[![Telegram][telegram-badge]][telegram-url]
[![CI Build][ci-badge]][ci-url]
[![Download][download-badge]][download-url]

</div>

[readme-cn-badge]: https://img.shields.io/badge/README-简体中文-blue.svg?style=for-the-badge&logo=readme
[readme-cn-url]: README.md
[telegram-badge]: https://img.shields.io/badge/Group-blue?style=for-the-badge&logo=telegram&label=Telegram
[telegram-url]: https://t.me/co2kernel
[ci-badge]: https://img.shields.io/github/actions/workflow/status/co2kernel/co2kernel_build/co2kernel_build.yml?style=for-the-badge&label=CI%20Build&logo=githubactions
[ci-url]: https://github.com/co2kernel/co2kernel_build/actions/workflows/co2kernel_build.yml
[download-badge]: https://img.shields.io/badge/download-stable-orange?style=for-the-badge&logo=github
[download-url]: https://github.com/co2kernel/co2kernel_release/releases/latest

<h1></h1>

#### 👾 Hacky Tricks
- Disabled Spectre-BHB mitigations to enable history-based branch prediction
- Uses optprobe to speed up KernelSU LKM and OnePlus kernel module Kprobe performance
- Spoofs official proc/version
- Spoofs official proc/config.gz
- Fixes ptrace msg leak
- Disables Nagle's algorithm for TCP connections to reduce latency
- Adds the NTSync driver for Wine
- Expands Nintendo Pro / Joy-Con controller support
- Device tree overwriting: patches the device tree on the kernel side without disabling AVB verification

| Device tree overwrite support | prjname | Modification |
| - | - | - |
| OnePlus Open | 22899 | Force global 120Hz while preserving LTPO behavior |
| OPPO Find N3 | 22003 / 22203 | No modification yet (requires user-submitted DTS and cmdline) |

#### 🦄 Compiler Optimizations
- Built with LTO=Thin
- Built with O3 optimization
- Enabled the LLVM Polly optimizer
- Applied LTO noinline to freezer_trap

#### 🖨️ Performance Gains by Debug Trade-offs
- Disabled avc logs
- Disabled KFENCE
- Disabled UBSAN
- Disabled I/O stat collection for BLK/BLKdev
- DRM: Removed debug logs
- PSI: Removed debug logs

#### ⚡ CPU Optimizations
- cpuidle: removed iowait from the menu
- PELT half-life reduced from 32ms to 16ms
- Reduced task migration overhead
- Default to the LSE atomic instruction set
- CRC-32 uses ARM64 acceleration

#### 🧻 Memory Optimizations
- lz4: v1.10.0 + ARMv8 acceleration
- Optimized mem* routines (~25%+ faster)
  - memcpy
  - memmove
  - memset
- mm: no reserved memory for user/admin login (~136 MB freed)
- arm64: 16-byte alignment for clear_page
- loop: improved writeback ring priority
- Minor zram optimizations
- SELinux: avoid dynamic memory allocations

#### 📀 Storage Optimizations
- Enforced none as the default I/O scheduler
- fs: 8b alignment

## 🍀 Special Thanks
This kernel integrates commits from **Sultan, arter97, Pzqqt, brokestar233, ztc1997, hfdem, and other kernel developers**

Special thanks to **Pzqqt, brokestar233, and Cloud_Yun** for their development guidance

*Order of kernel developers is not indicative of ranking*
