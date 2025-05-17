# 🧩 Yocto Project Documentation

The **Yocto Project** is a powerful framework for creating custom Linux distributions for embedded systems. It's designed to give you complete control over the Linux build process — including the kernel, toolchain, root filesystem, and packages.

This section introduces Yocto fundamentals and links to deeper guides on setting it up and customizing it.

---

## 📦 What is the Yocto Project?

Yocto is not a Linux distribution itself — it is a **build system** and **collection of tools** for creating your own Linux distribution tailored to your hardware.

It uses:
- **BitBake**: A task execution engine (similar to `make`)
- **Recipes**: Metadata describing how to build packages
- **Layers**: Modular collections of related recipes and configuration
- **Poky**: The reference distribution from the Yocto Project

---

## 🧠 Why Use Yocto?

✅ Highly customizable (kernel, toolchain, rootfs)  
✅ Great for commercial products  
✅ Modular through layers  
✅ Reproducible and scalable  
✅ Strong BSP (Board Support Package) ecosystem  
✅ Supported by many SoC vendors (NXP, Intel, etc.)

---

## 📚 Topics Covered in This Section

- [Yocto Setup](setup.md): Setting up Yocto, cloning Poky, choosing target machine
- [Layers](layers.md): What layers are, and how to add or create your own
- [Custom Recipes](custom-recipes.md): Writing your own BitBake recipes
- [Example Project](example-project.md): Building a minimal embedded Linux system

---

## 🔗 External Resources

- [Official Docs](https://www.yoctoproject.org/docs/)
- [Yocto Git Repos](https://git.yoctoproject.org/)
- [BitBake Manual](https://docs.yoctoproject.org/bitbake/)

---

> 💡 The Yocto Project is a steep but rewarding learning curve. It’s widely used in production-grade embedded Linux systems.
