# 🌲 Device Tree Overview

Device Trees describe the hardware layout to the Linux kernel, especially for ARM and RISC-V platforms. This guide explains the structure, usage, and customization of Device Tree files in embedded Linux.

---

## ❓ What Is a Device Tree?

- A **Device Tree** is a data structure that describes hardware components to the operating system.
- It separates hardware description from the kernel, enabling better reuse and modularity.
- Passed to the kernel at boot time by the bootloader (e.g., U-Boot).

---

## 📄 Device Tree Files

There are three types of files involved:

- **`.dts`**: Device Tree Source — main hardware description
- **`.dtsi`**: Device Tree Source Include — shared between devices
- **`.dtb`**: Device Tree Blob — compiled binary passed to the kernel

---

## 🧱 Device Tree Structure

A simple `example.dts`:

```dts
/dts-v1/;

/ {
    model = "My Embedded Board";
    compatible = "myvendor,myboard";

    memory@80000000 {
        device_type = "memory";
        reg = <0x80000000 0x10000000>;  // 256 MB RAM
    };

    cpus {
        cpu@0 {
            compatible = "arm,cortex-a7";
            reg = <0>;
        };
    };

    soc {
        uart0: serial@101f1000 {
            compatible = "arm,pl011";
            reg = <0x101f1000 0x1000>;
            interrupt-parent = <&intc>;
            interrupts = <5>;
        };
    };
};
```
---

## 🛠 Building Device Tree Blobs
From kernel source:

```bash
make ARCH=arm myboard_defconfig
make ARCH=arm myboard.dtb
```
You’ll find the compiled .dtb in:

```bash
arch/arm/boot/dts/myboard.dtb
```
---

## 🧩 Customizing Device Trees
You can:

- Add new hardware peripherals (GPIOs, SPI, I2C, UART)
- Enable or disable devices
- Override kernel default settings

To disable a device:

``dts
&uart0 {
    status = "disabled";
};
```
To enable and rename a device:

```dts
&spi1 {
    status = "okay";
    label = "spi-dev";
};
```
---

## ⚡ Device Tree Overlays
Some platforms (like Raspberry Pi, BeagleBone) support overlays — partial tree fragments that modify the base tree at runtime.

Not all kernels or boards support overlays.

---

## 🔍 Debugging
Use dtc (Device Tree Compiler) to decompile and inspect:

```bash
dtc -I dtb -O dts -o output.dts input.dtb
```
Examine /proc/device-tree/ on a running system:

```bash
cat /proc/device-tree/model
ls /proc/device-tree/soc/
```
---

## 📚 References
- [Device Tree Specification](https://www.devicetree.org/)
- [Elinux Device Tree Wiki](https://elinux.org/Device_Tree_Reference)
- [Kernel Docs: Device Trees](https://www.kernel.org/doc/html/latest/devicetree/index.html)

📚 Next:
- [Kernel Modules](modules.md)

