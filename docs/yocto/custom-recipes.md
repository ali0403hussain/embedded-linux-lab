# 🍳 Custom Recipes in Yocto

Yocto uses **recipes** to define how software packages are fetched, configured, compiled, and packaged. Custom recipes let you add or modify software in your embedded Linux image.

---

## 📜 What Is a Recipe?

A **BitBake recipe** (`.bb` file) is a set of instructions describing:

- Where to fetch the source code  
- How to configure and build the software  
- How to package the binaries  
- Dependencies and licenses

---

## 🗂 Recipe File Structure

Recipes typically live under layer directories like:

```plaintext
meta-my-layer/
└── recipes-example/
└── helloworld/
└── helloworld_1.0.bb
```

```python
The recipe filename format is:
```
<recipe-name>_<version>.bb

---

## 🔧 Basic Recipe Example

Here is a minimal recipe for a "Hello World" application:

```bitbake
SUMMARY = "Simple Hello World app"
LICENSE = "MIT"
SRC_URI = "file://helloworld.c"

S = "${WORKDIR}"

do_compile() {
    ${CC} ${CFLAGS} ${LDFLAGS} -o helloworld helloworld.c
}

do_install() {
    install -d ${D}${bindir}
    install -m 0755 helloworld ${D}${bindir}
}
```
---

## 🗃 Adding Source Files
Place source files (e.g., helloworld.c) in a files/ directory inside the recipe folder:

```palintext
meta-my-layer/
└── recipes-example/
    └── helloworld/
        ├── helloworld_1.0.bb
        └── files/
            └── helloworld.c
```
The SRC_URI = "file://helloworld.c" tells BitBake to copy the file during build.

---

## 🛠 Recipe Tasks
- do_fetch: Download sources
- do_unpack: Unpack sources
- do_patch: Apply patches
- do_compile: Build software
- do_install: Install files to image
- do_package: Create packages

You can override these tasks by defining functions in the recipe.

---

## 📦 Packaging and Dependencies
- Use DEPENDS to specify build-time dependencies
- Use RDEPENDS to specify runtime dependencies
- Define package contents with FILES_${PN}

Example:

```bitbake
DEPENDS = "libfoo"
RDEPENDS_${PN} = "libfoo"
FILES_${PN} = "/usr/bin/helloworld"
```
---

## 🧪 Testing Your Recipe
Add your layer to bblayers.conf then build the recipe:

```bash
bitbake helloworld
```
Check tmp/deploy/ipk (or rpm, deb depending on packaging) for output packages.

---

## 📚 Further Reading

- [Yocto Project Mega-Manual: Recipes](https://docs.yoctoproject.org/ref-manual/structure.html#meta-recipes-bsp)
- [BitBake Manual](https://docs.yoctoproject.org/bitbake/)

---

## ✅ Summary
Custom recipes let you integrate your software into Yocto builds. Start simple, then explore advanced features like patches, shared libraries, and complex dependencies.

---

## 📚 Next:
- [Example Yocto Project](example-project.md)

---