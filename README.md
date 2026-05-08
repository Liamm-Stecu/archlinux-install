# 🐧 Arch Linux Dual Boot Installation (archinstall)

> Install Arch Linux dual boot dengan Windows menggunakan `archinstall`.

---

# 📦 Persiapan

## Yang Dibutuhkan

- Flashdisk minimal 8GB
- ISO Arch Linux
- Rufus / Ventoy
- Koneksi internet

---

# 🔽 Download Arch Linux

Official website:

```txt
https://archlinux.org/download/
```

---

# 🔥 Membuat Bootable USB

## Menggunakan Rufus

1. Buka Rufus
2. Pilih flashdisk
3. Select ISO Arch Linux
4. Partition Scheme:
   - GPT → UEFI
   - MBR → BIOS / Legacy
5. Klik Start

---

# ⚠️ Persiapan Windows Dual Boot

## Disable Fast Startup

1. Control Panel
2. Power Options
3. Choose what the power buttons do
4. Disable:
   - `Turn on fast startup`

---

# 💽 Membuat Partisi Kosong

## Dari Windows

1. Tekan `Win + X`
2. Disk Management
3. Klik kanan drive Windows
4. Shrink Volume
5. Sisakan:
   - 30GB+
   - Akan menjadi `Unallocated`

---

# 🚀 Boot ke Arch Linux

Masuk boot menu:

| Brand | Tombol |
|---|---|
| ASUS | F8 |
| Acer | F12 |
| Lenovo | F12 |
| MSI | F11 |

Pilih:

```txt
UEFI: USB FLASHDISK
```

> Jangan pilih yang tanpa tulisan UEFI kalau mau install UEFI.

---

# 🌐 Connect WiFi

## Untuk Laptop / WiFi

Masuk iwctl:

```bash
iwctl
```

Scan WiFi:

```bash
device list
station wlan0 scan
station wlan0 get-networks
```

Connect WiFi:

```bash
station wlan0 connect NAMA_WIFI
```

Keluar:

```bash
exit
```

---

# 🌍 Test Internet

```bash
ping google.com
```

---

# 🕒 Sinkronisasi Waktu

```bash
timedatectl set-ntp true
```

---

# 💽 Cek Disk

```bash
lsblk
```

Contoh:

```txt
nvme0n1
sda
```

---

# 🧩 Membuat Partisi (Manual)

## Jalankan cfdisk

```bash
cfdisk /dev/nvme0n1
```

> Ganti sesuai disk kalian.

---

# 📁 Untuk UEFI Dual Boot

## Jangan Hapus EFI Windows

Biasanya:
- FAT32
- 100MB - 300MB

Contoh:

```txt
/dev/nvme0n1p1
```

Itu dipakai bersama Windows.

---

# ➕ Buat Root Partition Baru

Dari `Free Space`:

Create:
- Size:
  - 30GB+
- Type:
  - Linux filesystem

Contoh:

```txt
/dev/nvme0n1p5
```

---

# 💾 Optional Swap

Bisa buat:
- 2GB - 8GB
- Type:
  - Linux swap

---

# ✅ Write Partition

Pilih:

```txt
Write
```

Lalu:

```txt
yes
```

Kemudian:

```txt
Quit
```

---

# 🚀 Jalankan Archinstall

```bash
archinstall
```

---

# ⚙️ Konfigurasi Archinstall

---

# 🌍 Language

Pilih:

```txt
English
```

---

# ⌨️ Keyboard

Pilih:

```txt
us
```

---

# 🗺️ Mirror Region

Pilih:

```txt
Indonesia
```

atau:

```txt
Worldwide
```

---

# 💽 Disk Configuration

Pilih:

```txt
Manual Partitioning
```

---

# 🧱 Pilih Disk

Contoh:

```txt
nvme0n1
```

---

# 📁 Mount Point UEFI

## EFI Windows

Pilih partisi EFI Windows tadi.

Contoh:

```txt
nvme0n1p1
```

Set:

| Setting | Value |
|---|---|
| Mountpoint | `/boot/efi` |
| Format | `NO` |

> JANGAN FORMAT EFI kalau dual boot.

---

# 📂 Root Partition

Pilih partisi Linux yang tadi dibuat.

Contoh:

```txt
nvme0n1p5
```

Set:

| Setting | Value |
|---|---|
| Filesystem | ext4 |
| Mountpoint | `/` |
| Format | YES |

---

# 💾 Swap Partition (Optional)

Jika ada swap:

| Setting | Value |
|---|---|
| Filesystem | linuxswap |
| Mountpoint | none |

---

# 🖥️ Bootloader

Pilih:

```txt
GRUB
```

---

# 🌐 Hostname

Contoh:

```txt
archlinux
```

---

# 👤 Root Password

Isi password root.

---

# 👤 User Account

Buat user baru:

| Setting | Example |
|---|---|
| Username | marcel |
| Password | bebas |

Centang:
- sudo privileges

---

# 🌐 Network

Pilih:

```txt
Use NetworkManager
```

---

# 🖼️ Profile Desktop

Pilih sesuai kebutuhan.

Contoh:
- Hyprland
- KDE Plasma
- GNOME
- XFCE

---

# 🎮 Audio

Pilih:

```txt
pipewire
```

---

# 🚀 Install

Pilih:

```txt
Install
```

Tunggu sampai selesai.

---

# 🔚 Setelah Selesai

Pilih:

```txt
Yes
```

untuk:
- chroot

atau langsung:

```bash
reboot
```

---

# 💽 Cabut Flashdisk

Saat reboot:
- cabut flashdisk
- masuk ke GRUB

---

# ✅ Hasil Akhir

GRUB akan muncul:

```txt
Arch Linux
Windows Boot Manager
```

Dual boot berhasil 🎉
