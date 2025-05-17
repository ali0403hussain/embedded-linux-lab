# ⚙️ Setting Up the Yocto Project

Setting up Yocto can seem complex at first, but once the structure is understood, it becomes a powerful tool for embedded Linux development. This guide walks you through setting up the **Poky** reference distribution and preparing your host environment.

---

## 📦 Prerequisites

Ensure your development host is a Linux system with the following packages installed (example for Ubuntu/Debian):

```bash
sudo apt update && sudo apt install \
    gawk wget git-core diffstat unzip texinfo gcc \
    build-essential chrpath socat cpio python3 python3-pip \
    python3-pexpect xz-utils debianutils iputils-ping \
    libsdl1.2-dev xterm
```
---

## 📁 Directory Setup
Assume this structure inside your project repo:

```plaintext
dev/
└── third-party/
    └── yocto/
        ├── poky/
        └── meta-* (layers)
```
```bash
cd dev/third-party/yocto/
git clone https://git.yoctoproject.org/poky
cd poky
git checkout kirkstone  # or other stable release
```

---

## 🖥 Environment Setup
Yocto provides an environment script that configures the build environment:

```bash
source poky/oe-init-build-env
```
This sets up your working directory as build/ and drops you into a new shell with BitBake configured.

---

## 🛠 Configuring Yocto
After environment setup, edit:

conf/local.conf: Set machine architecture, parallel jobs, etc.

conf/bblayers.conf: Add paths to meta-layers

Example: conf/local.conf

```conf
MACHINE ?= "qemux86-64"
DISTRO ?= "poky"
PACKAGE_CLASSES ?= "package_rpm"
```

---

## 🚀 First Build
Try building a minimal image for QEMU:

```bash
bitbake core-image-minimal
```
This process may take time initially (1–2 hours). Artifacts will be placed in:

```swift
build/tmp/deploy/images/<machine>/
```
---

## 🧪 Run with QEMU (for QEMU targets)

```bash
runqemu qemux86-64
```
---

## 🧰 Build SDK
Generate a cross-compilation SDK:

```bash
bitbake core-image-minimal -c populate_sdk
```
This creates a self-contained toolchain installer in:

```bash
tmp/deploy/sdk/
```
Install it:

```bash
./tmp/deploy/sdk/poky-glibc-x86_64-core-image-minimal-*.sh
```
Then source the SDK environment script:

```bash
source /opt/poky/*/environment-setup-*
```
---

## ✅ Summary
- Clone poky and initialize the build environment.
- Configure the machine and layers.
- Use bitbake to build images and SDKs.
- Run using QEMU or flash to a physical device.

---

## 📚 Next:
- [Layers Overview](layers.md)
- [Custom Recipes](custom-recipes.md)
- [Example Yocto Project](example-project.md)

---