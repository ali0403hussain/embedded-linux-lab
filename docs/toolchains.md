# 🧰 Toolchains for Embedded Linux

Cross-compilation is a key part of embedded development. Since most embedded devices don’t have the power or environment to compile software themselves, we compile applications on a development machine (host) and run them on the embedded device (target).

---

## 🧠 What is a Toolchain?

A **toolchain** is a collection of development tools used to build software for a different architecture (e.g., ARM, MIPS, RISC-V). It usually includes:

- `gcc` or `clang`: The compiler
- `binutils`: Assembler, linker, etc.
- `libc`: C standard library (glibc, musl, uClibc)
- `gdb`: Debugger
- `pkg-config`: Metadata for libraries
- Sysroot: Target root filesystem headers and libraries

---

## 🔄 Cross vs Native Compilation

| Feature               | Native Compilation      | Cross Compilation                  |
|-----------------------|-------------------------|-------------------------------------|
| Compiling on          | Target itself           | Host machine                        |
| Performance           | Slow (on device)        | Fast (on host)                      |
| Use Case              | Prototyping, debugging  | Production, image building          |
| Tools Needed          | GCC, Make               | Cross-toolchain (e.g. arm-linux-gnueabihf-gcc) |

---

## 🧰 Toolchain Sources

You can obtain toolchains from several sources:

### 1. Prebuilt Toolchains

- **Linaro**: Optimized ARM toolchains  
  [https://www.linaro.org/downloads](https://www.linaro.org/downloads)

- **Bootlin Toolchains**  
  [https://toolchains.bootlin.com](https://toolchains.bootlin.com)

- **Xilinx, NXP, etc.** provide vendor-specific toolchains.

### 2. Build Your Own

- With **Buildroot** or **Yocto**, you can generate a custom toolchain:
  - In Buildroot: `make sdk`
  - In Yocto: `bitbake meta-toolchain`

### 3. System Package Managers (Not Ideal for Embedded)

```bash
sudo apt install gcc-arm-linux-gnueabihf
```
---

## 📦 Sysroot
A sysroot is a directory that mimics the target filesystem — it contains the headers and libraries the compiler uses when building code.

Set the sysroot in CMake or Makefiles to ensure correct linking:
```bash
cmake .. -DCMAKE_SYSROOT=/path/to/sysroot
```
---

## 🛠 Using Toolchains with CMake

```bash
# Toolchain file (e.g. arm-toolchain.cmake)
set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_SYSTEM_PROCESSOR arm)
set(CMAKE_C_COMPILER arm-linux-gnueabihf-gcc)
set(CMAKE_SYSROOT /path/to/sysroot)
```
```bash
cmake .. -DCMAKE_TOOLCHAIN_FILE=arm-toolchain.cmake
```
---

## ✅ Summary
Cross-compilation is essential in embedded systems.

Choose a toolchain matching your target’s architecture and C library.

Use sysroots and CMake toolchain files for clean, portable builds.

Yocto and Buildroot can both generate full SDKs.

---

## 📚 Next:

- [CMake Cross-Compilation](cmake-cross-compilation.md)
- Building the Kernel
    - [Yocto](yocto/setup.md) 
    - [buildroot](buildroot/setup.md)

---

