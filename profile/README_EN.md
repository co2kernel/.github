<div align = center>
<h1>CO₂Kernel</h1>

***C**ustom **O**nePlus **O**pen **K**ernel*

Customized kernel built for Hedwig/Xueying (OnePlus Open)

[📖 **zh-CN**](https://github.com/co2kernel/.github/blob/main/profile/README.md)
<h1></h1>
</div>

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
- Disabled KFENCE
- Disabled UBSAN
- Disabled I/O stat collection for BLK/BLKdev
- Disabled self-hosted debug
- DRM: Removed debug logs
- PSI: Removed debug logs
- SELinux: removed dependency on audit logs

#### 🔓 Performance Gains by Security Trade-offs
- Disabled Spectre-BHB mitigations to enable history-based branch prediction

#### ⚡ CPU Optimizations
- cpuidle: removed iowait from the menu
- PELT half-life reduced from 32 ms → 16 ms
- Reduced task migration overhead
- Default to LSE atomic instructions
- Relaxed alarmtimer to avoid blocking suspend

#### 📈 Network Optimizations
- Introduced "westwood-sub", a fork of "westwood-plus" with BBR-style convergence
- Set "westwood-sub" as the default TCP congestion algorithm
- Set "FQ-CoDel" as the default qdisc scheduler
- Disabled Nagle algorithm for TCP to reduce latency

#### 📦 Memory Optimizations
- lz4: v1.10.0 + ARMv8 acceleration
- Optimized memory functions (~25%+ faster):
  - memcpy
  - memmove
  - memset
- vmalloc: support huge virtual memory blocks
- mm: no reserved memory for user/admin login (~136 MB freed)
- arm64: 16b alignment for "clear_page()"
- loop: improved priority for zram writeback
- Minor zram optimizations
- SELinux: avoid dynamic memory allocations

#### 📀 Storage Optimizations
- Disabled all I/O schedulers
- fs: reduced cache to better utilize large RAM
- fs: 8b alignment

#### 🎮 Game Controller Supports
- Synced upstream controller compatibility list
- Synced upstream button mapping updates
- Added full support for Nintendo Pro / Joy-Con controllers

## 🍀 Special Thanks
This kernel integrates commits from **Sultan, arter97, Pzqqt, brokestar233, ztc1997, hfdem, and other kernel developers**

Special thanks to **Pzqqt, brokestar233, and Cloud_Yun** for their development guidance

*Order of kernel developers is not indicative of ranking*
