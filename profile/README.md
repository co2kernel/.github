<div align = center>
<h1>CO₂Kernel</h1>

***C**ustom **O**nePlus **O**pen **K**ernel*

为 Hedwig/Xueying (OnePlus Open) 编译的客制化内核

[![English][readme-en-badge]][readme-en-url]
[![Telegram][telegram-badge]][telegram-url]
[![CI Build][ci-badge]][ci-url]
[![Download][download-badge]][download-url]

</div>

[readme-en-badge]: https://img.shields.io/badge/README-English-blue.svg?style=for-the-badge&logo=readme
[readme-en-url]: README_EN.md
[telegram-badge]: https://img.shields.io/badge/Group-blue?style=for-the-badge&logo=telegram&label=Telegram
[telegram-url]: https://t.me/co2kernel
[ci-badge]: https://img.shields.io/github/actions/workflow/status/co2kernel/co2kernel_build/co2kernel_build.yml?style=for-the-badge&label=CI%20Build&logo=githubactions
[ci-url]: https://github.com/co2kernel/co2kernel_build/actions/workflows/co2kernel_build.yml
[download-badge]: https://img.shields.io/badge/download-stable-orange?style=for-the-badge&logo=github
[download-url]: https://github.com/co2kernel/co2kernel_release/releases/latest

<h1></h1>

#### 👾 内核侧 root 实现 
- 伪装官方 proc/version
- 伪装官方 proc/config.gz
- KernelSU Next: latest release
- KernelSU Scope Minimized Hooks: v1.4
- 启用 tmpfs 拓展属性以支持 Mountify
- 修复 ptrace msg leak

#### 🌳 内核侧设备树覆写
- 无需关闭 AVB verify, 使用 overwriter 修补设备树
- OnePlus Open (22899)
  - 强制全局 120Hz 且保留 LTPO 特性
- OPPO Find N3 (22003, 22203)
  - 暂无修改 (需要用户提交 dts 与 cmdline)

#### 🦄 编译器优化
- 使用 LTO=Thin 优化编译
- 使用 O3 优化编译
- 使用 llvm Polly 优化器
- 对 freezer_trap 作 LTO noinline 处理

#### 🖨️ 妥协调试效率换取的性能提升
- 禁用 avc logs
- 禁用 KFENCE
- 禁用 UBSAN
- BLK/BLKdev 不收集 io stat
- 去除 drm 中的 debug
- 去除 psi 中的 debug
- 关闭 self-hosted debug

#### 🔓 妥协安全性换取的性能提升
- 禁用 Spectre-BHB 缓解措施以启用基于历史的分支预测

#### ⚡ CPU 优化
- cpuidle: 去除 menu 的 iowait
- PELT 半衰期 32ms → 16ms
- 减少任务迁移开销
- 默认使用 LSE 原子指令集
- CRC-32 使用 ARM64 加速
- 相对宽容的 alarmtimer, 避免阻止 suspend

#### 📈 网络栈优化
- 引入采用 bbr 收敛方式的 "westwood-plus" 算法变种 "westsood-sub"
- 将 "westwood-sub" 作为默认的 TCP 拥塞算法
- 将 "FQ-CoDel" 作为默认的数据包队列调度器
- TCP 链接禁用 Nagle 算法以降低延迟

#### 🧻 内存优化
- lz4: v1.10.0 + ARMv8 加速
- 优化的 mem* (~25%+ faster)
  - memcpy
  - memmove
  - memset
- kvmalloc: 让 kmalloc 的快速路径更快
- vmalloc: 支持大块虚拟内存
- mm: 不为 user/admin 登录而保留内存 (~136m)
- arm64: clear_page 对齐 16b
- loop: 提高回写环优先级
- 小幅 zram 优化
- selinux: 避免动态内存分配

#### 📀 存储优化
- 添加 SSG I/O 调度器，并强制将其设为默认的 I/O 调度器
- fs: 减少缓存以发挥大内存的作用
- fs: 对齐 8b

#### 🎮 游戏优化
- 同步上游手柄适配列表
- 同步上游手柄按钮支持
- 支持 Nintendo Pro / Joy-con 手柄
- 为 Wine 添加 NTSync 驱动

#### 📦 LXC 容器支持
- 可选 LXC 容器支持

#### 🪦 "墓碑" 模块支持
- 添加 Re:Kernel 用户态 "墓碑" 模块支持

## 🍀 特别感谢
此内核合并了来自 **Sultan, arter97, Pzqqt, brokestar233, ztc1997, hfdem 等内核开发者** 的提交

感谢 **Pzqqt, brokestar233, Cloud_Yun** 提供了开发指导

*内核开发者们的排名不分先后*
