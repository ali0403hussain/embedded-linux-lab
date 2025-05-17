# 🧩 Linux Kernel Modules

Kernel modules are pieces of code that can be loaded and unloaded into the kernel at runtime. This allows adding functionality without recompiling the kernel.

---

## ⚙️ What Is a Kernel Module?

- Dynamically loadable code into the running kernel.
- Used for hardware drivers, file systems, and custom extensions.
- File extension: `.ko` (kernel object)

---

## 🧪 Simple Example Module

Create `hello.c`:

```c
#include <linux/init.h>
#include <linux/module.h>
#include <linux/kernel.h>

MODULE_LICENSE("GPL");
MODULE_AUTHOR("You");
MODULE_DESCRIPTION("A simple Hello World module");

static int __init hello_init(void) {
    printk(KERN_INFO "Hello, kernel!\n");
    return 0;
}

static void __exit hello_exit(void) {
    printk(KERN_INFO "Goodbye, kernel!\n");
}

module_init(hello_init);
module_exit(hello_exit);
```
---

## 🛠 Building the Module
Makefile:

```make
obj-m += hello.o

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```
Build with:

```bash
make
```
This creates hello.ko.

--- 

## 📦 Loading and Unloading
To load:

```bash
sudo insmod hello.ko
dmesg | tail
```
To remove:

```bash
sudo rmmod hello
dmesg | tail
```
Check module list:

```bash
lsmod
```
---

## 📁 Installing in Embedded System
Cross-compile your module:

```bash
export ARCH=arm
export CROSS_COMPILE=arm-linux-gnueabihf-
make -C /path/to/kernel M=$(PWD) modules
```
Install to rootfs:

```bash
make INSTALL_MOD_PATH=/path/to/rootfs modules_install
```
---

## 🔎 Debugging Tips
- Use dmesg for kernel log messages.
- Check /proc/modules and /sys/module/
- Use modinfo hello.ko to inspect metadata.

---

## 🧰 Best Practices
- Use MODULE_LICENSE("GPL") to avoid taint warnings.
- Isolate hardware-specific logic in modules.
- Clean up resources properly in module_exit.

---

## 📚 References
- [Linux Kernel Module Programming Guide](https://tldp.org/LDP/lkmpg/2.6/html/)
- [Kernel Docs: Modules](https://www.kernel.org/doc/html/latest/kbuild/modules.html)

---

✅ Done with Kernel Section   
📚 Next up: GPIO Example