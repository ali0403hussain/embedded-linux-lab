# 🧪 Buildroot Example Project

This example demonstrates how to create a minimal embedded Linux system using Buildroot, run it with QEMU, and include a custom application.

---

## 🎯 Project Goals

- Build a minimal root filesystem with BusyBox  
- Include a simple C application (`hello`)  
- Run the system on QEMU using a virtual x86 target

---

## 🧱 Project Structure

```plaintext
buildroot/
external/
└── myapp/
├── Config.in
├── myapp.mk
└── src/
└── hello.c
board/
└── myboard/
└── rootfs-overlay/
└── etc/
└── motd
```
---

## 📝 Step-by-Step Guide

### 1. Clone Buildroot

```bash
git clone https://github.com/buildroot/buildroot.git
cd buildroot
```
### 2. Create External Package (myapp)
Create directory:

```bash
mkdir -p ../external/myapp/src
```
Write the application:

src/hello.c:

```c
#include <stdio.h>
int main() {
    printf("Hello from Buildroot custom app!\n");
    return 0;
}
```
myapp.mk:

```make
MYAPP_VERSION = 1.0
MYAPP_SITE = $(TOPDIR)/../external/myapp/src
MYAPP_SITE_METHOD = local

define MYAPP_BUILD_CMDS
    $(MAKE) -C $(@D)
endef

define MYAPP_INSTALL_TARGET_CMDS
    $(INSTALL) -m 0755 $(@D)/hello $(TARGET_DIR)/usr/bin/hello
endef

$(eval $(generic-package))
```
Config.in:

```make
config BR2_PACKAGE_MYAPP
    bool "MyApp - Hello App"
    help
      A simple hello-world app.
```
### 3. Configure Buildroot

```bash
make qemu_x86_defconfig
make menuconfig
```
Then:

- Enable your external package:

```rust
Package selection for the target  --->
  [*] myapp
```
- Specify rootfs overlay:

```sql
System configuration  --->
  (../board/myboard/rootfs-overlay) Root filesystem overlay directories
```
### 4. Add Overlay File (Optional)
Create a custom message in motd:

```bash
mkdir -p ../board/myboard/rootfs-overlay/etc
echo "Welcome to Buildroot Project!" > ../board/myboard/rootfs-overlay/etc/motd
```
### 5. Build the System

```bash
make
```
### 6. Run with QEMU

```bash
qemu-system-x86_64 -kernel output/images/bzImage \
    -append "console=ttyS0" \
    -nographic \
    -drive file=output/images/rootfs.ext2,format=raw,index=0,media=disk
```
You should see the login prompt and message from motd.

### 7. Run Your App
Login as root (no password), then:

```bash
hello
```
Output:

```vbnet
Hello from Buildroot custom app!
```
----

## ✅ Summary
This example demonstrates how to:
- Use Buildroot to create a minimal Linux system
- Add and compile a custom application
- Use rootfs overlays for configuration
- Boot and test the system using QEMU

---

## 📚 Learn more in:

- [Buildroot Manual](https://buildroot.org/downloads/manual/manual.html)
- [Custom Packages Guide](https://buildroot.org/downloads/manual/manual.html#adding-packages)

---