# 🧩 Step 1 — Disk Partitioning

This step prepares your drive for a modern Arch Linux installation using:

- UEFI
- GPT
- A separate EFI partition
- A single encrypted root partition (LUKS2)

The result is a clean and minimal layout designed for FDE, Btrfs, UKI, Secure Boot, and TPM2 workflows.

---

# 📀 1. Boot Into the Arch ISO

Make sure you are using UEFI mode.  
Verify network connectivity:

```bash
ping archlinux.org
````

List your disks:

```bash
lsblk
```

Identify your target drive (example: `nvme0n1` or `sda`).

---

# 🧩 2. Partition the Drive

Use **cfdisk** to create the required GPT partitions:

```bash
cfdisk /dev/<drive_name>
```

Create the following:

### ✔ Partition 1 — EFI System Partition (ESP)

* **Size:** 1024 MiB
* **Type:** EFI System
* **Format later as:** FAT32

### ✔ Partition 2 — Root Partition (Encrypted)

* **Size:** Rest of the disk
* **Type:** Linux filesystem
* This will later be encrypted with LUKS2 and contain all Btrfs subvolumes.

After creating both partitions:

* Select **Write**
* Confirm
* Quit cfdisk

---

# 📌 3. Verify the Layout

Run:

```bash
lsblk
```

You should now see something like:

```
nvme0n1
 ├─nvme0n1p1   1G   EFI System Partition
 └─nvme0n1p2   rest Linux filesystem (to be encrypted)
```

If everything looks correct, proceed to the encryption step in the next section.

---

➡️ **Next: [02 — LUKS Encryption](02-luks-encryption.md)**


