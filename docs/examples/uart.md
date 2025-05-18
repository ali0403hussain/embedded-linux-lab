# 🧭 UART in Embedded Linux

UART (Universal Asynchronous Receiver/Transmitter) is one of the most common serial communication protocols in embedded systems. It allows point-to-point communication between devices.

---

## 🧠 What is UART?

- Full-duplex, asynchronous serial communication.
- Uses TX (transmit), RX (receive), and GND lines.
- Commonly used for debugging, communication with microcontrollers, sensors, GPS, etc.

---

## 🔧 Enabling UART

Make sure UART is enabled on your board:

- Raspberry Pi: Enable `/boot/config.txt` → `enable_uart=1`
- BeagleBone: Check `/boot/uEnv.txt`
- Other boards: Consult the device tree or board documentation.

---

## 📂 Accessing UART in Linux

UART ports show up as:

```bash
/dev/ttyS0      # Traditional serial port
/dev/ttyAMA0    # ARM-specific UART
/dev/ttyUSB0    # USB-to-Serial converter
/dev/ttyACM0    # USB CDC ACM device
```
Use dmesg | grep tty to see what’s connected.

---

## 📟 Simple Communication with minicom or screen
Install:

```bash
sudo apt install minicom
```
Run:

```bash
minicom -b 115200 -D /dev/ttyUSB0
```
Or with screen:

```bash
screen /dev/ttyUSB0 115200
```
---
## 💻 UART Programming in C
```c
#include <fcntl.h>
#include <termios.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    int uart0 = open("/dev/ttyUSB0", O_RDWR | O_NOCTTY);

    struct termios options;
    tcgetattr(uart0, &options);
    cfsetispeed(&options, B115200);
    cfsetospeed(&options, B115200);

    options.c_cflag |= (CLOCAL | CREAD);
    tcsetattr(uart0, TCSANOW, &options);

    char *msg = "Hello UART\n";
    write(uart0, msg, strlen(msg));

    close(uart0);
    return 0;
}
```
Compile with:

```bash
gcc uart.c -o uart
```
---

## 📚 Useful Tools
- minicom, screen, picocom — for terminal access
- setserial, stty — configure serial port parameters
- dmesg, ls /dev/tty* — device discovery

---

## 🛡 Permissions
You may need to add your user to the dialout group:

```bash
sudo usermod -aG dialout $USER
```
Then log out and log back in.

---

## 🧪 Test Setup
To test UART loopback:
1. Connect TX and RX on a USB-UART adapter.
2. Use a terminal tool to send and receive data.
3. Or write a simple echo program.

---

## 📚 References
- [Writing a UART driver for Linux](https://www.marcusfolkesson.se/blog/writing-a-uart-driver-for-linux/)
- [Linux Serial Ports Using C/C++](https://blog.mbedded.ninja/programming/operating-systems/linux/linux-serial-ports-using-c-cpp/)

---

✅ Done with UART.
📚 [Next up: I2C Example](i2c.md)

---