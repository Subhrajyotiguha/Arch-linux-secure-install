# 📦 Step 3 — Base System Installation

With the encrypted Btrfs filesystem mounted and subvolumes in place, we can now install the base Arch Linux system and generate essential configuration files.

---

## 📥 1. Update the Package Mirrorlist (Optional but Recommended)

Select fast mirrors:

```bash
reflector --country <country_name> --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
````
<country_name> is to be changed with your actual country name
Or use worldwide fast mirrors:

```bash
reflector --latest 20 --sort rate --save /etc/pacman.d/mirrorlist
```

---

## 🏗️ 2. Install Base Packages

Use `pacstrap` to install the minimal Arch base:

```bash
pacstrap -K /mnt base linux linux-firmware btrfs-progs nano
```

If using Intel/AMD microcode,just add with the pacstrap:

```bash
intel-ucode
# or
amd-ucode
```

---

## 📝 3. Generate `fstab`

```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

Verify:

```bash
cat /mnt/etc/fstab
```

Ensure all Btrfs subvolumes + EFI partition appear correctly with your mount options.

---

## 🧬 4. Chroot Into the New System

```bash
arch-chroot /mnt
```

You are now inside your new Arch Linux installation.

---

## 🌐 5. Set Locale and Time

### Set timezone:

```bash
ln -sf /usr/share/zoneinfo/<continent>/<region> /etc/localtime
```
make sure that the dates are correct by using:
'''bash
date
'''
### Sync hardware clock:

```bash
hwclock --systohc
```

### Enable locale:

Edit `/etc/locale.gen`:

```bash
nano /etc/locale.gen
```

Uncomment:

```
en_US.UTF-8 UTF-8
```
or uncomment the one as per your specific region

Generate locales:

```bash
locale-gen
```

Create `/etc/locale.conf`:

```bash
echo "LANG=en_US.UTF-8" > /etc/locale.conf
```

---

## 🧑‍💻 6. Set Hostname

```bash
echo "<your-hostname>" > /etc/hostname
```

Add matching hosts entries:

```bash
cat >> /etc/hosts <<EOF
127.0.0.1    localhost
::1          localhost
127.0.1.1    <your-hostname>.localdomain <your-hostname>
EOF
```

---

## 🔐 7. Set Root Password

```bash
passwd
```

Choose a strong one.

---

## ⚙️ 8. (Optional) Install Network Tools

```bash
pacman -S networkmanager
systemctl enable NetworkManager
```

---

## ✔ Completed

You have installed:

* Arch base system
* Kernel
* Firmware
* Btrfs utilities
* Locale & hostname
* Network manager (optional)

Your system is ready for:

➡️ **SNext — [Initramfs (mkinitcpio) + UKI preset generation](04-mkinitcpio-uki.md)**
 
