# Getting Started with Embedded Linux Lab

Welcome to the Embedded Linux Lab! This guide will help you set up your environment and get started with building and experimenting with Embedded Linux systems.

---

## Prerequisites

- A Linux development machine (Ubuntu/Debian recommended)
- Basic familiarity with Linux command line
- Git installed (`git --version`)
- Required tools: `gcc`, `make`, `cmake`, `curl`, `tar`, `wget`, `git`, `python3`, etc.
- Docker (optional, for containerized builds)

---

## Cloning the Repository

Clone this repository along with its submodules:

```bash
git clone --recurse-submodules https://github.com/ali0403hussain/embedded-linux-lab.git
cd embedded-linux-lab
```
If you already cloned without --recurse-submodules, run:

```bash
git submodule update --init --recursive
```

## Building Examples

We use CMake for building the example projects. To build:

```bash
mkdir build && cd build
cmake ../dev/examples
make
```

## Setting Up Yocto Project
The Yocto Project is a powerful build system for embedded Linux. It is included as a submodule inside dev/third-party/yocto.

To initialize and update:
```bash
cd dev/third-party/yocto
git checkout dunfell   # or desired branch
```
For full setup and build instructions, see the [Yocto Setup Guide](https://docs.yoctoproject.org/brief-yoctoprojectqs/index.html).

## Setting Up Buildroot
Buildroot is another popular embedded Linux build system, included as a submodule inside dev/third-party/buildroot.

To initialize and update:
```bash
cd dev/third-party/buildroot
git checkout 2025.02  # or desired version
```
Refer to the [Buildroot Setup Guide](https://buildroot.org/downloads/manual/manual.html) for detailed instructions.

## Next Steps
Read through the [Embedded Linux Overview](embedded-linux-overview.md) to get familiar with the ecosystem.

Explore the [Toolchains](toolchains.md) page to understand cross-compilation basics.

Dive into kernel development via the Kernel Docs and device tree topics.

Start experimenting with real hardware examples in dev/examples/.