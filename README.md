# MaskOS Kernel

This repository contains the `PKGBUILD` and associated files (kernel configuration, patches) for building the hardened Linux kernel specifically tailored for **MaskOS**.

MaskOS is a TTY-only, hardened, and privacy-focused operating system. The kernel used in MaskOS is custom-built with a strong emphasis on security, anonymity, and reducing the attack surface.

## Key Features & Hardening:
* **Custom Kernel Configuration (`.config`):** Based on the official Arch Linux kernel configuration, meticulously refined to include advanced security features.
* **Kernel Address Space Layout Randomization (KASLR):** Enabled to randomize kernel memory locations, making exploit development significantly harder.
* **Hardened Usercopy:** Enhanced security for copying data between kernel and user space to prevent various memory-related vulnerabilities.
* **Strict Kernel Memory Protections (RWX, /dev/mem):** Implemented to prevent arbitrary code execution and unauthorized memory access within the kernel.
* **SLAB/SLUB Hardening:** Protections against heap corruption vulnerabilities in kernel memory allocators.
* **Stack Protector Strong:** Robust defense against stack overflow attacks.
* **TorNet and Process Isolation Support:** Includes necessary kernel options (e.g., `TPROXY` for Netfilter, `USER_NS` for Firejail) to support MaskOS's core privacy and isolation features.
* **Reduced Attack Surface:** Removal of unnecessary debugging features, tracing mechanisms, and unneeded drivers/modules.

## Building the MaskOS Kernel:
To build the `linux-maskos` kernel package, ensure you are on an Arch-based system with `base-devel` installed.

1.  **Prerequisites:** Ensure you have the `base-devel` package group installed (if not already):
    ```bash
    sudo pacman -S base-devel
    ```
2.  **Clone this repository:**
    ```bash
    git clone [https://github.com/maskos-dev/maskos-kernel.git](https://github.com/maskos-dev/maskos-kernel.git)
    cd maskos-kernel
    ```
3.  **Build the kernel package:**
    ```bash
    makepkg -s
    ```
    * This command will download the official Linux kernel source, apply our custom `.config` and any patches, and compile it into a `linux-maskos-*.pkg.tar.zst` package.
    * You might be prompted during `makepkg` to confirm new kernel options if the base `config` has changed significantly or if `oldconfig` is used.
4.  **Install the package (for testing on an Arch-based system):**
    ```bash
    sudo pacman -U linux-maskos-*.pkg.tar.zst
    ```
    * **Note:** This is for testing the kernel on a development machine. The MaskOS installer will handle kernel installation on the target system.

## Contribution:
Contributions to the MaskOS kernel are welcome!

## License:
This project, being a derivative work of the Linux kernel, is licensed under the **GNU General Public License, Version 2 only (GPLv2)**.
See the `LICENSE` file for full details.
