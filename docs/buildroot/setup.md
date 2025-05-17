# ⚙️ Buildroot Setup

This guide walks you through setting up Buildroot for your embedded Linux development.

---

## 📥 Downloading Buildroot

You can get Buildroot either by cloning the Git repository or downloading a release tarball.

- **Clone the repository:**

```bash
git clone https://github.com/buildroot/buildroot.git
cd buildroot
```
Download a release: 
Visit [Buildroot releases](https://buildroot.org/download.html) and download a stable tarball.

---

## 🛠 Selecting a Configuration
Buildroot uses predefined configurations for many popular boards and architectures.

- List available configs:

```bash
ls configs/
```
- Load a default config (example for QEMU x86_64):

```bash
make qemu_x86_64_defconfig
```
---

## 📝 Customizing the Configuration
- Launch the menuconfig interface:

```bash
make menuconfig
```
- Use arrow keys and Enter to navigate.
- Enable or disable packages, select toolchain options, kernel versions, etc.
- Save your configuration (.config file) before exiting.

---
 
## 🔧 Building the System
- Start the build:

```bash
make
```
- This may take some time depending on your system and selected packages.
- Build artifacts will be placed in output/images/.

---

## 🔄 Cleaning Builds
- To clean the build directory but keep config:

```bash
make clean
```
- To remove everything (including config):

```bash
make distclean
```
---

## ⚙️ Toolchain Options
- Buildroot can build its own cross-toolchain or use an external one.
- Configure this under Toolchain in menuconfig.

---

## 🧩 Adding Your Own Packages
- Create package description files (.mk and Config.in) under package/.
- Add your package to menuconfig and dependencies.

---

## 📚 References
- [Buildroot manual: Getting Started](https://buildroot.org/downloads/manual/manual.html#getting-started)

---

## ✅ Summary
Setting up Buildroot involves choosing a target configuration, customizing the build with menuconfig, and running make to generate your embedded Linux system.

---

## 📚 Next:

- [Buildroot Customization](customization.md)
- [Buildroot Example Project](example-project.md)

