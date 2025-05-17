# 🧱 Yocto Layers Overview

Yocto uses **layers** to organize metadata, recipes, and configuration. Layers enable modularity and reuse by separating concerns and allowing you to add or remove functionality easily.

---

## 🗂 What Is a Layer?

- A **layer** is a directory containing BitBake recipes, configuration files, and classes.  
- Layers can be BSPs (Board Support Packages), software stacks, or custom application layers.  
- Each layer has a `conf/layer.conf` file describing its priority and dependencies.

---

## 📚 Common Layers

- `meta-poky`: Core Yocto metadata and tools  
- `meta-yocto-bsp`: Board support packages for common hardware  
- `meta-openembedded`: Additional recipes for extra packages  
- `meta-<vendor>`: Vendor-specific BSPs or custom layers

---

## 📁 Layer Directory Structure

```plaintext
meta-example/
├── conf/
│ └── layer.conf
├── recipes-core/
│ └── busybox/
│ └── busybox_%.bbappend
├── recipes-kernel/
│ └── linux/
│ └── linux-yocto_%.bbappend
└── classes/
└── custom_class.bbclass
```
---

## ➕ Adding Layers to Your Build

Edit `conf/bblayers.conf` in your build directory to add layers:

```conf
BBLAYERS ?= " \
  /path/to/poky/meta \
  /path/to/poky/meta-poky \
  /path/to/poky/meta-yocto-bsp \
  /path/to/meta-openembedded/meta-oe \
  /path/to/meta-yourlayer \
"
```
---

## 🆕 Creating Your Own Layer
Yocto provides a script to create a new layer skeleton:
```bash
yocto-layer create meta-my-layer
```
---

## ⚠️ Layer Priority and Conflicts
Layers have priorities set in layer.conf.

Higher priority layers override recipes or configuration from lower ones.

Use layer priorities carefully to manage conflicts.

---

## 💡 Tips
Keep BSP layers separate from application layers.

Use community layers like meta-openembedded for additional software.

Document your layers well for maintainability.

---

## ✅ Summary
Layers are the modular building blocks of Yocto projects. Understanding layers helps you customize and extend your embedded Linux system efficiently.

---

## 📚 Next:
- [Custom Recipes](custom-recipes.md)
- [Example Yocto Project](example-project.md)

---