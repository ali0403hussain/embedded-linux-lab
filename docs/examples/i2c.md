# 🔗 I2C in Embedded Linux

I2C (Inter-Integrated Circuit) is a two-wire communication protocol used for low-speed peripheral communication. It's widely used to connect sensors, EEPROMs, RTCs, and more.

---

## 🧠 What is I2C?

- Two lines: **SCL** (clock) and **SDA** (data).
- Supports multiple masters and slaves.
- Each device has a unique 7- or 10-bit address.
- Slower than SPI but requires fewer wires.

---

## 🔌 I2C on Linux

Linux provides I2C support through the `/dev/i2c-*` interface.

### 🔍 List available I2C buses:

```bash
ls /dev/i2c-*
```
---

## 🛠 Install I2C tools:
```bash
sudo apt install i2c-tools
```
---

## 🔍 Detect devices on a bus:
```bash
sudo i2cdetect -y 1
```
This scans bus 1 for connected devices.

---

## 📚 Reading/Writing I2C Registers
🔍 Read a register:
```bash
sudo i2cget -y 1 0x50 0x00
```
This reads from device at address 0x50, register 0x00.

---

## ✍ Write a value:
```bash
sudo i2cset -y 1 0x50 0x00 0xFF
```
---

## 💻 I2C in C (Userspace API)
```c
#include <linux/i2c-dev.h>
#include <sys/ioctl.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    int file = open("/dev/i2c-1", O_RDWR);
    int addr = 0x50;

    ioctl(file, I2C_SLAVE, addr);

    char buf[1] = { 0x00 }; // Register to read
    write(file, buf, 1);
    read(file, buf, 1);
    
    printf("Value: 0x%02x\n", buf[0]);
    close(file);
    return 0;
}
```
Compile with:

```bash
gcc i2c.c -o i2c
```
---

## 📋 Device Tree Configuration
To enable I2C on boards like Raspberry Pi or BeagleBone, you may need to:
- Edit /boot/config.txt to enable overlays.
- Load kernel modules: i2c-dev, i2c-bcm2835, etc.

---

## 🛡 Permissions
Like UART and GPIO, access to /dev/i2c-* may require root or group membership.

---

📚 References
- [Linux I2C Subsystem](https://www.kernel.org/doc/html/latest/i2c/index.html)

---

✅ Done with I2C.
📚 [Next: SPI Example](spi.md)

---