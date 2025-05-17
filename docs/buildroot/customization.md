# 🛠 Buildroot Customization

Once Buildroot is set up, you can tailor it to meet your project’s requirements. This guide covers ways to customize your system, from rootfs layout to kernel and packages.

---

## 🧱 Filesystem Layout

You can choose the root filesystem format in `make menuconfig`:

```plaintext
Filesystem images --->
[*] ext4 root filesystem
[ ] tar root filesystem
[ ] cpio root filesystem
```

Set size, compression options, or even enable read-only filesystems.

---

## 🐧 Kernel Customization

- You can enable kernel build within Buildroot:

```plaintext
Kernel --->
[*] Linux Kernel
(linux) Kernel version
(/path/to/defconfig) Configuration file
```

- To modify kernel config:

```bash
make linux-menuconfig
```
- To apply patches, place them in:

```bash
board/<your_board>/linux/
```
And configure patch directory in menuconfig.

---

## 📦 Custom Packages
To add your own package:
- 1. Create a folder under package/ (e.g., package/myapp/)
- 2. Add two files:

myapp.mk:
```make
MYAPP_VERSION = 1.0
MYAPP_SITE = $(TOPDIR)/../myapp
MYAPP_SITE_METHOD = local

define MYAPP_BUILD_CMDS
    $(MAKE) -C $(@D)
endef

define MYAPP_INSTALL_TARGET_CMDS
    $(INSTALL) -m 0755 $(@D)/myapp $(TARGET_DIR)/usr/bin/
endef

$(eval $(generic-package))
```
Config.in:

```make
config BR2_PACKAGE_MYAPP
    bool "myapp"
    help
      Simple custom application
```
 - 3. Add your package to the main package/Config.in file.

 ---

 ## 🧰 Init System
Select init system (BusyBox, systemd, etc.) in System configuration → Init system.

You can also create init scripts in board/<your_board>/rootfs-overlay/etc/init.d/.

---

## 🪝 Rootfs Overlays
To add custom files to the root filesystem, create an overlay directory:

```bash
mkdir -p board/myboard/rootfs-overlay/etc/
echo "Welcome to Embedded Linux!" > board/myboard/rootfs-overlay/etc/motd
```
Then point to it in menuconfig:

```sql
System configuration  --->
    (board/myboard/rootfs-overlay) Root filesystem overlay directories
```
---

## 🎯 Post-Build Scripts
Use post-build scripts to tweak the rootfs after it's built:

```pgsql
System configuration  --->
    (/path/to/post-build.sh) Custom scripts to run after creating target filesystem
```
Example post-build.sh:

```bash
#!/bin/sh
echo "Customizing rootfs..."
touch $TARGET_DIR/etc/custom-flag
```

----

## References
- [Buildroot Manual – Customization](https://buildroot.org/downloads/manual/manual.html#_customizing_the_generated_filesystem)
- [Package Infrastructure Guide](https://buildroot.org/downloads/manual/manual.html#adding-packages)

---

## ✅ Summary
Buildroot makes it easy to customize your embedded Linux system via overlays, custom packages, kernel options, and filesystem tweaks. Use this power to match your exact project needs.

📚 Next:

- [Buildroot Example Project](example-project.md)

---