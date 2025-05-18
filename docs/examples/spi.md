# 🔄 SPI in Embedded Linux

SPI (Serial Peripheral Interface) is a high-speed synchronous serial communication protocol. It’s commonly used to communicate with sensors, ADCs, DACs, displays, and flash memory.

---

## 🧠 What is SPI?

- Full duplex, synchronous communication.
- Lines: **MOSI**, **MISO**, **SCLK**, **CS** (Chip Select).
- Master initiates all communication.

---

## 📂 Accessing SPI in Linux

SPI devices show up under `/dev/spidevB.C`, where:
- `B` = SPI bus number
- `C` = Chip Select (CS) line

> Example: `/dev/spidev0.0`

---

## 🔧 Enable SPI on Common Boards

### Raspberry Pi:
Edit `/boot/config.txt`:

```bash
dtparam=spi=on
```
Then reboot and check with:

```bash
ls /dev/spidev*
```
---

## 🛠 SPI Tools
Install:

```bash
sudo apt install spi-tools
```
Use spidev_test (provided in kernel source under tools/spi/) to test devices.

---

## 💻 SPI Programming in C
```c
#include <linux/spi/spidev.h>
#include <fcntl.h>
#include <sys/ioctl.h>
#include <stdio.h>
#include <unistd.h>

int main() {
    int fd = open("/dev/spidev0.0", O_RDWR);
    if (fd < 0) return -1;

    uint8_t tx[] = { 0x9F };  // Example command: read JEDEC ID
    uint8_t rx[3] = { 0 };

    struct spi_ioc_transfer tr = {
        .tx_buf = (unsigned long)tx,
        .rx_buf = (unsigned long)rx,
        .len = sizeof(tx) + sizeof(rx),
        .speed_hz = 500000,
        .bits_per_word = 8,
    };

    ioctl(fd, SPI_IOC_MESSAGE(1), &tr);
    printf("Response: %02X %02X %02X\n", rx[0], rx[1], rx[2]);
    close(fd);
    return 0;
}
```
Compile with:

```bash
gcc spi.c -o spi
```
---

## ⚙️ Configurable Parameters
You can use ioctl() to configure:
- SPI mode (0, 1, 2, 3)
- Speed (Hz)
- Bits per word
- LSB/MSB first

Example:

```c
uint8_t mode = SPI_MODE_0;
ioctl(fd, SPI_IOC_WR_MODE, &mode);
```
---

## 🛡 Permissions
SPI access may require root or membership in the spi group (if defined).

---

## 📚 References
- [Linux SPI Subsystem](https://www.kernel.org/doc/html/latest/spi/index.html)
- [spidev_test](https://github.com/torvalds/linux/blob/master/tools/spi/spidev_test.c)

