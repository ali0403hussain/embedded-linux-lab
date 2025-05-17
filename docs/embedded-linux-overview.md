# 📘 Overview of Embedded Linux

Embedded Linux is a customized version of the Linux operating system designed to run on embedded systems — devices that are not traditional computers but still need software to function.

This document provides a high-level understanding of what Embedded Linux is, where it’s used, and the components that make up a typical embedded system.

---

## What Is Embedded Linux?

Embedded Linux is a lightweight, configurable version of the Linux kernel, designed to run on devices with limited resources (CPU, memory, power).

Unlike desktop Linux, embedded Linux systems:
- Are often headless (no GUI)
- Boot directly into a single application or service
- Are tailored to specific hardware and use cases

---

## Common Use Cases

Embedded Linux is used in a wide range of devices:

- 📱 Consumer electronics (TVs, routers, smartwatches)
- 🚗 Automotive systems (infotainment, ADAS)
- 🏭 Industrial control systems (PLCs, HMIs)
- 🏥 Medical devices
- 🛰️ Aerospace and defense systems
- 🔐 IoT and edge computing devices

---

## Key Components

An Embedded Linux system typically includes:

- **Bootloader** (e.g., U-Boot): Initializes hardware and loads the Linux kernel
- **Linux Kernel**: Core of the OS, customized for the target hardware
- **Device Tree**: Describes hardware layout to the kernel
- **Root Filesystem (rootfs)**: Contains system libraries, binaries, and configuration
- **Init System**: Initializes user space (e.g., systemd, busybox `init`)
- **User Applications**: Custom apps or services for the device

---

## Build Systems

There are several tools used to build custom Embedded Linux systems:

- **Yocto Project**: Highly customizable and professional-grade system builder
- **Buildroot**: Simple, fast, and effective tool for smaller embedded systems
- **OpenWRT / PTXdist / PetaLinux**: Specialized build tools for networking, Xilinx, etc.

---

## Why Use Embedded Linux?

✅ Open Source and license-friendly  
✅ Flexible and modular  
✅ Community-driven support  
✅ Vast ecosystem (toolchains, BSPs, drivers)  
✅ Easy integration with networking, file systems, protocols, etc.

---

## 🧮 Comparison: Embedded Linux vs RTOS vs Bare-Metal

| Feature             | Embedded Linux        | RTOS                    | Bare-Metal Programming     |
|---------------------|-----------------------|-------------------------|----------------------------|
| Real-Time Support   | With PREEMPT-RT patch | Built-in                | Deterministic (manual)     |
| Size                | Larger (~10MB+)       | Very small (<1MB)       | Extremely small (KBs)      |
| Complexity          | Higher                | Medium                  | Low (code-driven)          |
| Ecosystem           | Rich                  | Moderate                | Minimal (MCU-specific)     |
| Networking Stack    | Full (TCP/IP, etc.)   | Often minimal or add-on | None (requires integration)|
| Boot Time           | High (~5s–20s)        | Low (<1s)               | Very low (<100ms)          |
| Development Effort  | High (build systems)  | Moderate                | High (bare metal code)     |
| Portability         | High (across SoCs)    | Depends on RTOS         | Very low (hardware-tied)   |
| Use Case Examples   | Routers, HMIs, cameras| Drones, sensors, IoT    | Simple sensors, drivers    |

---

### 📝 Summary

- **Embedded Linux** is great for feature-rich applications and complex stacks.
- **RTOS** is suited for real-time, mid-complexity embedded tasks.
- **Bare-Metal** is best for ultra-low-power, high-speed, or extremely resource-constrained systems.

---

## Learn More

- [Yocto Overview](yocto/index.md)
- [Buildroot Overview](buildroot/index.md)
- [Toolchains](toolchains.md)
- [CMake Cross Compilation](cmake-cross-compilation.md)

---

> 💡 Embedded Linux gives you the power of Linux with the constraints and performance required for embedded systems.
