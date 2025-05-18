# 🔌 GPIO in Embedded Linux

GPIO (General Purpose Input/Output) allows you to control digital signals on your hardware pins. This is commonly used to toggle LEDs, read button states, etc.

---

## 🧠 What is GPIO?

- GPIO pins are simple digital input/output pins.
- Can be controlled through userspace interfaces like `/sys/class/gpio` or `/dev/gpiochip*` (newer).

---

## 📂 Sysfs Interface (Legacy)

Older kernels use `/sys/class/gpio`.

### 🛠 Example: Toggle GPIO

```bash
# Export GPIO pin (e.g., GPIO17)
echo 17 > /sys/class/gpio/export

# Set direction
echo out > /sys/class/gpio/gpio17/direction

# Set value to HIGH
echo 1 > /sys/class/gpio/gpio17/value

# Set value to LOW
echo 0 > /sys/class/gpio/gpio17/value

# Unexport when done
echo 17 > /sys/class/gpio/unexport
```

⚠️ Sysfs GPIO is deprecated since Linux 4.8. Use character device interface (/dev/gpiochipN) if possible.

---

## 🆕 libgpiod Interface (Modern Way)
Use libgpiod for modern GPIO access.

1. ✅ Install:
``bash
sudo apt install libgpiod-dev gpiod
``
2. 📘 Example: Read GPIO input
```bash
gpioget gpiochip0 17
```
3. 📘 Example: Set GPIO output
```bash
gpioset gpiochip0 17=1
```
---

## 💻 Code Example (C)
```c
#include <gpiod.h>
#include <stdio.h>

int main() {
    struct gpiod_chip *chip = gpiod_chip_open_by_name("gpiochip0");
    struct gpiod_line *line = gpiod_chip_get_line(chip, 17);
    gpiod_line_request_output(line, "gpio_example", 0);

    gpiod_line_set_value(line, 1);  // HIGH
    sleep(1);
    gpiod_line_set_value(line, 0);  // LOW

    gpiod_chip_close(chip);
    return 0;
}
```
Compile with:

```bash
gcc gpio.c -lgpiod -o gpio
```
---

## 📚 GPIO Numbering
- SoC GPIO numbers vs. Board pin numbers (e.g., Raspberry Pi GPIO 17 = physical pin 11).
- Refer to your board’s documentation or use pin mapping tools.

---

## 🛡 Permissions
Accessing GPIO may require root or group membership (gpio, dialout, etc.).

---

## 📚 References
- [libgpiod Git](https://git.kernel.org/pub/scm/libs/libgpiod/libgpiod.git/)
- [Sysfs GPIO (deprecated)](https://www.kernel.org/doc/Documentation/gpio/sysfs.txt)
- [Elinux GPIO](https://elinux.org/GPIO)

---

✅ Done with GPIO.
📚 Next: [UART Example](uart.md)

---