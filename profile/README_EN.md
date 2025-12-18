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

#### 👾 Kernel-side Root Implementation
- Spoofs official proc/version
- Spoofs official proc/config.gz
- KernelSU Next: latest release
- KernelSU Scope Minimized Hooks: v1.4
- Enables tmpfs extended attributes to support "Mountify"
- Fixes ptrace msg leak

#### 🌳 Kernel-side Device Tree Overwriting
- Patches device tree using "Overwriter" without disabling AVB verify
- OnePlus Open (22899):
  - Enforces 120Hz while preserving LTPO
- OPPO Find N3 (22003, 22203):
  - No modification yet (DTS and cmdline needed)

#### 🦄 Compiler Optimizations
- Compiled with LTO = Thin
- Compiled with O3 optimization
- Enabled LLVM Polly optimizer
- LTO noinline to "freezer_trap"

#### 🖨️ Performance Gains by Debug Trade-offs
- Disabled avc logs
- Disabled KFENCE
- Disabled UBSAN
- Disabled I/O stat collection for BLK/BLKdev
- Disabled self-hosted debug
- DRM: Removed debug logs
- PSI: Removed debug logs

#### 🔓 Performance Gains by Security Trade-offs
- Disabled Spectre-BHB mitigations to enable history-based branch prediction

#### ⚡ CPU Optimizations
- cpuidle: removed iowait from the menu
- PELT half-life reduced from 32 ms → 16 ms
- Reduced task migration overhead
- Default to LSE atomic instructions
- CRC-32 uses ARM64 acceleration
- Relaxed alarmtimer to avoid blocking suspend

#### 📈 Network Optimizations
- Introduced "westwood-sub", a fork of "westwood-plus" with BBR-style convergence
- Set "westwood-sub" as the default TCP congestion algorithm
- Set "FQ-CoDel" as the default qdisc scheduler
- Disabled Nagle algorithm for TCP to reduce latency

#### 🧻 Memory Optimizations
- lz4: v1.10.0 + ARMv8 acceleration
- Optimized memory functions (~25%+ faster):
  - memcpy
  - memmove
  - memset
- kvmalloc: make kmalloc fast path real fast path
- vmalloc: support huge virtual memory blocks
- mm: no reserved memory for user/admin login (~136 MB freed)
- arm64: 16b alignment for "clear_page()"
- loop: improved priority for zram writeback
- Minor zram optimizations
- SELinux: avoid dynamic memory allocations

#### 📀 Storage Optimizations
- Added SSG I/O scheduler and enforce it as the default scheduler
- fs: reduced cache to better utilize large RAM
- fs: 8b alignment

#### 🎮 Gaming Optimizations
- Synced upstream controller compatibility list
- Synced upstream button mapping updates
- Added full support for Nintendo Pro / Joy-Con controllers
- Added NTSync driver for Wine

#### 📦 LXC Container Support
- Optional LXC container support

#### 🪦 "Tombstone" Modules Support
- Added Re:Kernel for supporting userspace "tombstome" modules

## 🍀 Special Thanks
This kernel integrates commits from **Sultan, arter97, Pzqqt, brokestar233, ztc1997, hfdem, and other kernel developers**

Special thanks to **Pzqqt, brokestar233, and Cloud_Yun** for their development guidance

*Order of kernel developers is not indicative of ranking*
