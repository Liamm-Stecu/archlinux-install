# 🐧 Arch Linux Dual Boot Installation Guide

> Install Arch Linux dual boot dengan Windows menggunakan UEFI mode.

---

# 📦 Persiapan Sebelum Install

## Yang Dibutuhkan

- Flashdisk minimal 8GB
- File ISO Arch Linux
- Aplikasi bootable USB:
  - Rufus (Windows)
  - Ventoy
  - Balena Etcher

---

# 🔽 Download Arch Linux

Download ISO resmi:

```txt
https://archlinux.org/download/
```

---

# 🔥 Membuat Bootable USB

## Menggunakan Rufus

1. Buka Rufus
2. Pilih flashdisk
3. Select ISO Arch Linux
4. Partition scheme:
   - GPT → untuk UEFI
5. Start

---

# ⚠️ Persiapan Dual Boot Windows

## Disable Fast Startup Windows

1. Control Panel
2. Power Options
3. Choose what power buttons do
4. Disable:
   - `Turn on fast startup`

---

# 💽 Membuat Partisi Kosong

## Dari Windows

1. Tekan `Win + X`
2. Pilih:
   - Disk Management
3. Klik kanan drive Windows
4. Pilih:
   - Shrink Volume
5. Sisakan minimal:
   - 30GB+

Nanti akan menjadi:
- `Unallocated Space`

---

# 🚀 Boot ke Arch Linux

## Masuk Boot Menu

Biasanya:

| Brand | Tombol |
|---|---|
| ASUS | F8 |
| Acer | F12 |
| Lenovo | F12 |
| MSI | F11 |
| Gigabyte | F12 |

Pilih:
- UEFI USB

---

# 🌐 Cek Internet

## WiFi

```bash
iwctl
```

Masuk ke iwctl:

```bash
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect NAMA_WIFI
exit
```

## Test Internet

```bash
ping google.com
```

---

# 🕒 Sinkronisasi Waktu

```bash
timedatectl set-ntp true
```

---

# 💽 Melihat Disk

```bash
lsblk
```

Contoh disk:

```txt
nvme0n1
sda
```

---

# 🧩 Membuat Partisi Arch Linux

## Masuk cfdisk

```bash
cfdisk /dev/nvme0n1
```

> Ganti `nvme0n1` sesuai disk kalian.

---

# 📁 Partisi yang Dibutuhkan

## Root Partition

Buat:
- Type:
  - Linux filesystem
- Size:
  - 20GB+

## Swap Partition (Opsional)

Buat:
- Type:
  - Linux swap
- Size:
  - 2GB - 8GB

---

# 🧱 Format Partisi

## Format Root

```bash
mkfs.ext4 /dev/nvme0n1pX
```

## Format Swap

```bash
mkswap /dev/nvme0n1pY
swapon /dev/nvme0n1pY
```

> Ganti `X` dan `Y` sesuai nomor partisi.

---

# 📂 Mount Partisi

## Mount Root

```bash
mount /dev/nvme0n1pX /mnt
```

## Mount EFI Windows

```bash
mkdir -p /mnt/boot/efi
mount /dev/nvme0n1p1 /mnt/boot/efi
```

> Biasanya partisi EFI Windows adalah `p1`

---

# 📦 Install Base System

```bash
pacstrap /mnt base linux linux-firmware nano sudo networkmanager grub efibootmgr
```

---

# 🧬 Generate fstab

```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

---

# 🔐 Masuk ke Arch

```bash
arch-chroot /mnt
```

---

# 🌍 Set Timezone

## Indonesia WIB

```bash
ln -sf /usr/share/zoneinfo/Asia/Jakarta /etc/localtime
hwclock --systohc
```

---

# 🌐 Setup Locale

Edit locale:

```bash
nano /etc/locale.gen
```

Uncomment:

```txt
en_US.UTF-8 UTF-8
```

Generate locale:

```bash
locale-gen
```

Buat locale.conf:

```bash
echo "LANG=en_US.UTF-8" > /etc/locale.conf
```

---

# 🖥️ Hostname

## Set Hostname

```bash
echo "archlinux" > /etc/hostname
```

Edit hosts:

```bash
nano /etc/hosts
```

Isi:

```txt
127.0.0.1 localhost
::1 localhost
127.0.1.1 archlinux.localdomain archlinux
```

---

# 🔑 Set Password Root

```bash
passwd
```

---

# 👤 Membuat User

## Tambah User

```bash
useradd -m -G wheel -s /bin/bash marcel
passwd marcel
```

---

# ⚡ Enable Sudo

```bash
EDITOR=nano visudo
```

Uncomment:

```txt
%wheel ALL=(ALL:ALL) ALL
```

---

# 🌐 Enable Internet

```bash
systemctl enable NetworkManager
```

---

# 🪟 Install GRUB Dual Boot

## Install GRUB

```bash
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=Arch
```

## Install os-prober

```bash
pacman -S os-prober
```

Edit config:

```bash
nano /etc/default/grub
```

Uncomment:

```txt
GRUB_DISABLE_OS_PROBER=false
```

Generate config:

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

---

# 🚪 Exit & Reboot

```bash
exit
umount -R /mnt
reboot
```

---

# ✅ Setelah Reboot

GRUB akan muncul dengan pilihan:

- Arch Linux
- Windows Boot Manager

---

# 🎉 Arch Linux Berhasil Diinstall

Welcome to ArchLinux
