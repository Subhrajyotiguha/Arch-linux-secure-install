# 🌐 About This Project

Welcome to my complete **Arch Linux Secure Boot + UKI + TPM2** installation guide.
This project documents a modern, hardened, and fully reproducible Arch Linux setup built on:

* 🔐 **Full Disk Encryption (LUKS2)**
* 🧩 **Btrfs subvolumes and clean filesystem layout**
* 🛡️ **Secure Boot with custom keys (No Microsoft keys)**
* 🔏 **Unified Kernel Images (UKI) — direct EFI boot, no bootloader**
* 🔒 **TPM2-bound decryption for auto-unlock**
* 🧱 **Kernel hardening + AppArmor LSM stacking**
* 📦 **Flatpak sandboxing for desktop security**

My goal is to create one of the **cleanest, most secure, minimalist, and modern** Arch Linux installation guides available — without unnecessary complexity, without legacy tooling, and without outdated GRUB workflows.

This project is inspired by real-world secure boot chains used in:

* Android Verified Boot
* ChromeOS
* Systemd's modern EFI boot model
* Hardened Linux distributions

…and brings those concepts into a fully DIY Arch environment.

---

#☝️ Project Purpose

This guide exists to:

* Document a **reliable and repeatable** personal Arch install
* Share a working example of **UKI-first boot flow**
* Demonstrate **custom Secure Boot keys** and **signed kernels**
* Show how to integrate TPM2-based unlocking safely
* Provide a **reference** for others who want a hardened Arch setup
* Make modern Linux boot technologies more accessible

This is not meant to be a “copy paste blindly” tutorial — instead, it aims to educate, explain, and provide clarity on every step so anyone can understand what’s happening under the hood.

---

# ✍️ Philosophy

This project follows a few simple principles:

### • **Minimalism**

Only modern, clean components: systemd, UKI, sbctl, TPM2, Btrfs.
No GRUB. No legacy bootloaders. No bloat.

### • **Security by design**

The boot chain is cryptographically sealed from firmware → kernel.
If anything changes, TPM refuses to unlock.

### • **Reproducibility**

Every command and configuration is documented.
No magic, no guesswork.

### • **Education-first**

This guide explains concepts, not just commands.
You should understand *why* every part exists.

### • **Modern Arch Linux workflows**

Using technologies that Arch supports natively today, not workflows from 2016.

---

# 🛠️ Technologies Used

* **systemd-boot (optional; direct UKI boot used ideally)**
* **UKI (Unified Kernel Images)**
* **sbctl Secure Boot key management**
* **TPM2 & systemd-cryptenroll**
* **Btrfs with subvolumes**
* **mkinitcpio with UKI presets**
* **AppArmor + LSM stacking**
* **Kernel hardening flags**
* **Flatpak sandboxing**

---

# 🧑‍💻 About Me

I’m a Linux user and security enthusiast who enjoys:

* Understanding things deeply rather than using them blindly
* Building strong, modern systems from scratch
* Learning how the boot chain and OS internals truly work
* Exploring security, cryptography, and system design
* Writing clean, minimal documentation so others can follow along

This project started as my personal installation notes.
Now, it has evolved into a public guide for anyone who wants to build a **hardened Arch Linux system from the ground up**.

---

# 🤝 Contributions

Contributions, suggestions, and improvements are always welcome.
You can:

* Open a **pull request**
* Report issues
* Suggest improvements
* Submit cleaned-up configs
* Add missing explanations

All constructive input is appreciated.

---
