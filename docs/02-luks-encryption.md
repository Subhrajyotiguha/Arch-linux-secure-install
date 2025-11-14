# 🔐 Step 2 — LUKS Encryption

In this step, we initialize full-disk encryption using **LUKS2**, unlock it, format it as Btrfs, and prepare directories for subvolumes.

---

## 🔒 1. Format the EFI Partition

```bash
mkfs.fat -F32 /dev/<EFI-partition>
````

This prepares the 1 GiB EFI System Partition created earlier.

---

## 🔐 2. Encrypt the Root Partition (LUKS2)

```bash
cryptsetup luksFormat /dev/<root-partition>
```

⚠️ **Enter the passphrase VERY CAREFULLY.**
This is the main disk encryption password.

---

## 🔓 3. Open the Encrypted Volume

```bash
cryptsetup open /dev/<root-partition> <luks-partition-name>
```

Example:

```bash
cryptsetup open /dev/nvme0n1p2 cryptroot
```

This creates:

```
/dev/mapper/<luks-partition-name>
```

---

## 📦 4. Format the LUKS container as Btrfs

```bash
mkfs.btrfs /dev/mapper/<luks-partition-name>
```

---

## 📁 5. Create Temporary Mount

```bash
mount /dev/mapper/<luks-partition-name> /mnt
```

---

## 🧩 6. Create Btrfs Subvolumes

```bash
btrfs su cr /mnt/@
btrfs su cr /mnt/@home
btrfs su cr /mnt/@log
btrfs su cr /mnt/@cache
btrfs su cr /mnt/@.snapshots
```

---

## 🔄 7. Unmount Before Final Mounting

```bash
umount /mnt
```

---

### 📌 Btrfs Mount Options Explained
**now before you mount the partitions,get to know these mount options as they are used to optimize the disks and the filesystem (you can add more or less as per your specific needs !)**
- **noatime** — Disables access-time writes, reducing SSD wear and improving performance.  
- **ssd** — Enables Btrfs SSD optimizations for faster metadata and write handling.  
- **compress=zstd:3** — Transparent compression using Zstandard for better speed and reduced disk usage.  
- **space_cache=v2** — Modern free-space cache improving performance and reliability.  
- **discard=async** — Safe asynchronous TRIM for SSDs, maintaining long-term performance without slowdowns.
---

## 📌 8. Final Mounted Layout (With Subvolumes)

### Mount the root subvolume:

```bash
mount -o noatime,ssd,compress=zstd:3,space_cache=v2,discard=async,subvol=@ \
/dev/mapper/<luks-partition-name> /mnt
```

### Create mount points:

```bash
mkdir -p /mnt/{boot,home,var/log,var/cache,.snapshots}
```

### Mount the EFI partition:

```bash
mount /dev/<EFI-partition> /mnt/boot
```

### Mount other subvolumes:

```bash
mount -o noatime,ssd,compress=zstd:3,space_cache=v2,discard=async,subvol=@home \
/dev/mapper/<luks-partition-name> /mnt/home

mount -o noatime,ssd,compress=zstd:3,space_cache=v2,discard=async,subvol=@log \
/dev/mapper/<luks-partition-name> /mnt/var/log

mount -o noatime,ssd,compress=zstd:3,space_cache=v2,discard=async,subvol=@cache \
/dev/mapper/<luks-partition-name> /mnt/var/cache

mount -o noatime,ssd,compress=zstd:3,space_cache=v2,discard=async,subvol=@snapshots \
/dev/mapper/<luks-partition-name> /mnt/.snapshots
```

---

## ✔ 9. Verify Everything

```bash
lsblk
```

Make sure the EFI partition and all Btrfs subvolumes are mounted correctly.

---

➡️ **Next: [03 — Base Installation](03-base-install.md)**


