# 🚀 Example Yocto Project

This example guides you through creating a basic Yocto project to build a simple embedded Linux image.

---

## 🏗 Project Setup

1. **Clone the Poky repository** (Yocto reference distribution):

```bash
git clone git://git.yoctoproject.org/poky.git
cd poky
```
2. **Checkout a stable branch** (e.g., dunfell):

```bash
git checkout dunfell
```
3. **Initialize the build environment:**

```bash
source oe-init-build-env
```
This creates a build directory with config files.

---

## 📝 Configuration Files
- conf/local.conf: Customize build options, e.g., MACHINE, DISTRO
- conf/bblayers.conf: Define layers to include in build

Example changes in local.conf:

```conf
MACHINE ?= "qemarm"
```
---

## ➕ Adding Layers
Add required layers to bblayers.conf, for example:

```conf
BBLAYERS ?= " \
  /path/to/poky/meta \
  /path/to/poky/meta-poky \
  /path/to/poky/meta-yocto-bsp \
  /path/to/meta-openembedded/meta-oe \
  /path/to/meta-my-layer \
"
```
---

## 🧰 Building an Image
To build a basic image:

```bash
bitbake core-image-minimal
```
Or build your own custom image if you have one defined.

---

## 📂 Output Artifacts
After building, images and packages are in:

```swift
tmp/deploy/images/<machine>/
```
You’ll find:

- Kernel images
- Root filesystem images
- SDK installers
- Package files

## 🛠 Testing Your Image
- Use an emulator like QEMU to boot the image.
- Deploy image to target hardware via SD card, USB, or network.

Example QEMU boot command for qemarm:

```bash
runqemu qemarm
```
---

## 📝 Customizing Your Project
- Add custom recipes in your layers
- Modify local.conf and bblayers.conf as needed
- Use BitBake commands like bitbake -c menuconfig virtual/kernel for kernel config

---

##  📚 References
- [Yocto Project Quick Start](https://docs.yoctoproject.org/brief-yoctoprojectqs/)
- [Poky Git Repository](https://git.yoctoproject.org/poky/)

---

## ✅ Summary
This example project provides a foundation to explore building embedded Linux images with Yocto. Extend it by adding layers, recipes, and customization to fit your hardware and software needs.

---