# Reverse Engineering 逆向工程学习仓库（中文说明）

> 本仓库 fork 自 **[mytechnotalent/Reverse-Engineering](https://github.com/mytechnotalent/Reverse-Engineering)**（DC540 Discord 社区的逆向工程教学项目）。
>
> 上游原版英文索引（600+ 节课的完整课程表）见 **[README.md](README.md)**；本文件是面向中文使用者的仓库导览与本地练习工程说明。

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

---

## 一、这是什么

一个**系统性的逆向工程 / 底层安全学习仓库**，配套 DC540（DEF CON 540）每周课程，覆盖从数字电路、汇编语言、操作系统内核到 IoT 固件的完整链路。

内容分三类：

| 类别 | 内容 |
|---|---|
| **课程课件与索引** | x86 / x64 / ARM32 / ARM64 / RISC-V / WebAssembly / Rust / 嵌入式 / Windows 内核 等 20+ 门课程的逐节链接 |
| **可编译的练习工程** | 仓库根目录下的 `0x000X-*` Visual Studio 工程（Windows 汇编与 Win32 API 实践） |
| **硬件与资料** | Fritzing 电路图、配套 PDF 电子书、课程用图 |

---

## 二、仓库内练习工程（Windows / Visual Studio）

这些是可直接编译运行的实践代码，按课时编号排列：

| 目录 | 语言 | 核心内容 |
|---|---|---|
| `0x0001-hello_world-x64` / `-x86` | x64 / x86 **汇编（MASM）** | 最小可运行 Windows 程序：调用 `MessageBoxA` 弹窗 + `PostQuitMessage` 退出，含手写影子栈（shadow stack）处理 |
| `0x0006-directories` | C | `CreateDirectory` / `RemoveDirectory` 创建与删除目录 |
| `0x0007-copyfile` | C | `CopyFile` 文件复制 |
| `0x0010-movefile` | C | `MoveFile` 文件移动 / 重命名 |
| `0x0011-createfile` | C | `CreateFile` 获取文件句柄 + `CloseHandle` |
| `0x0012-writefile` | C | `WriteFile` 写入文件 |
| `0x0013-readfile` | C | `ReadFile` 读取文件 |

> **关于 `*-x64 Debug` / `*-x86 Debug` 目录**：这些是 Visual Studio 的构建产物目录，被一并提交进了仓库，不是源码目录。

### 编译与运行

1. **环境**：Visual Studio 2022，安装工作负载「**使用 C++ 的桌面开发**」；
   汇编工程还需在 VS Installer 的「单个组件」中勾选 **MASM**（用于 x64/x86 的汇编程序）。
2. 用 VS 打开对应目录下的 `*.sln`；
3. 选择 `Debug | x64` 或 `Debug | x86` 配置，`Ctrl+Shift+B` 生成，`F5` 运行。

### ⚠️ 运行前必读（示例含硬编码路径）

部分示例写死了绝对路径，直接运行会失败，需先准备环境：

| 工程 | 依赖路径 |
|---|---|
| `0x0006-directories` | 在 `C:\` 下创建 / 删除 `mydir` |
| `0x0007-copyfile` | 需要已存在的 `C:\temp\test1.txt` |
| `0x0010-movefile` | 需要已存在的 `C:\temp\test1.txt` |
| `0x0011-createfile` | 需要已存在的 `C:\temp\` 目录 |
| `0x0012-writefile` / `0x0013-readfile` | 同上，读写 `C:\temp\` 下的文件 |

建议先手动建立 `C:\temp\` 目录与 `test1.txt`，再逐个运行。

---

## 三、硬件与电路图

| 文件 | 说明 |
|---|---|
| `dynamic RE schematic.fzz` / `.png` | 动态逆向（运行时分析）实验电路图 |
| `static RE schematic.fzz` / `.png` | 静态逆向（固件提取）实验电路图 |
| `oled and button schematic.fzz` / `.png` | OLED 屏 + 按键模块电路图 |

`.fzz` 为 [Fritzing](https://fritzing.org/) 工程文件，可用 Fritzing 打开编辑；`.png` 为导出预览图。

## 四、配套资料

| 文件 | 说明 |
|---|---|
| `reversing-for-everyone.pdf` | 逆向工程入门电子书（约 25 MB） |
| `Ouroboros_How_It_Works.pdf` | Ouroboros 加密引擎原理说明 |
| `Reverse Engineering.png` | 课程主视觉图 |
| `DC540 Angels Of Death.png` / `K Background.png` / `REDAH.png` | 课程与社区用图 |
| `badges/` | 项目徽章资源 |

---

## 五、课程总览（上游索引摘要）

完整课表与逐节链接请见 [README.md](README.md)，主要课程包括：

| 方向 | 课程 |
|---|---|
| **x86 / x64** | x86 Course、x64 Course（汇编基础、寄存器、栈与堆、PE 结构、调试器） |
| **ARM** | ARM-32 Course 1/2、ARM-32 Project Course、ARM-64 Course |
| **RISC-V** | Hacking RISC-V Course、RP2350 RISC-V Assembler Course |
| **WebAssembly** | Wasm Course、Embedded Wasm（UART Echo / Blinky / Button / Servo） |
| **Rust** | Hacking Rust、Hacking Embedded Rust（含 microbit）、RP2350 Rust Course |
| **嵌入式 / 汇编** | Embedded Assembler Course、Embedded Hacking Course、AVR Assembler Course、RP2350 ARM Assembler Course |
| **Windows 安全** | Hacking Windows Course、Windows Process Lifecycle、Windows Kernel Debugging、Windows Indirect Syscall |
| **其他语言与平台** | Go Hacking Course、Pico Hacking Course、Hacking Bits Course、Reverse Engineering Data Course |

### 上游配套工具与项目

- **[REA](https://github.com/mytechnotalent/rea)** — Reverse Engineering Assistant，自主逆向分析框架
- **Ghidra 插件** — [G-AVR](https://github.com/mytechnotalent/G-AVR)、[G-Pulley](https://github.com/mytechnotalent/G-Pulley)
- **The Ouroboros Engine** — 自研加密引擎
- **Windows 工具链** — Hacking Windows、内核调试、间接系统调用
- **IoT / CTF** — OPERATION COLD IRON（Act I–X）、OPERATION TELESCREEN、DC540 Hacking Challenge `0x00001`–`0x00009`
- **STEM 教学** — Python For Kids、Python Zero To Hero、TinyGPT、Minimal Harness

---

## 六、建议的学习路径

1. **补基础**：x86/x64 课程的数字系统 → 寄存器 → 栈 / 堆 → 汇编指令；
2. **动手编译**：按本仓库 `0x000X-*` 顺序做练习，先读源码，再用调试器（x64dbg / WinDbg）单步对照；
3. **静态分析**：用 Ghidra / IDA 反编译自己编译出的二进制，与源码逐行对照；
4. **动态分析**：配合 `dynamic RE schematic` 进入硬件层面的 JTAG / UART 调试；
5. **进阶**：Windows 内核调试、间接系统调用，以及 RISC-V / Wasm 方向。

---

## 七、免责声明

本仓库所有代码与资料**仅用于安全技术学习与研究**。示例涉及文件系统与进程操作 API，
请在**隔离环境（虚拟机 / 专用测试机）**中运行，勿用于任何未授权的系统。

---

## 八、许可与致谢

- 本项目遵循 **[Apache License 2.0](LICENSE)**。
- 原始项目：**[mytechnotalent/Reverse-Engineering](https://github.com/mytechnotalent/Reverse-Engineering)**，作者 **Kevin Thomas**（[@mytechnotalent](https://github.com/mytechnotalent)）。
- 社区：DC540 Discord 逆向工程学习社区。
- 本仓库为个人学习用 fork，中文说明由仓库维护者补充。
