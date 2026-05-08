# 🐧 Install Arch Linux Dual Boot (archinstall + Ventoy)

> Install Arch Linux dual boot dengan Windows pake cara paling gampang (`archinstall`).

---

# 📦 Persiapan

Yang dibutuhkan:

- Flashdisk minimal 8GB
- ISO Arch Linux
- Aplikasi Ventoy
- Internet

---

# 🔽 Download Arch Linux

Download ISO:

```txt
https://archlinux.org/download/
```

---

# 🔥 Membuat Bootable USB (Ventoy)

## 1. Download Ventoy

```txt
https://www.ventoy.net/
```

## 2. Install Ventoy ke Flashdisk

- Buka Ventoy
- Pilih flashdisk
- Klik:
  
```txt
Install
```

> Semua isi flashdisk akan kehapus.

---

# 📂 Masukkan ISO Arch

Setelah Ventoy selesai:

- buka flashdisk
- copy file ISO Arch Linux ke flashdisk

Selesai ✅

---

# ⚠️ Persiapan Windows

## Disable Fast Startup

1. Control Panel
2. Power Options
3. Choose what the power buttons do
4. Disable:

```txt
Turn on fast startup
```

---

# 💽 Membuat Partisi Kosong

## Dari Windows

1. Tekan:

```txt
Win + X
```

2. Pilih:

```txt
Disk Management
```

3. Klik kanan drive Windows
4. Pilih:

```txt
Shrink Volume
```

5. Sisakan:
- 30GB+
- nanti jadi:

```txt
Unallocated
```

---

# 🚀 Boot ke Ventoy

Masuk boot menu:

| Brand | Tombol |
|---|---|
| ASUS | F8 |
| Acer | F12 |
| Lenovo | F12 |
| MSI | F11 |

Pilih:

```txt
UEFI: Ventoy
```

> WAJIB pilih yang ada tulisan UEFI.

---

# ▶️ Boot ISO Arch

Di menu Ventoy:

- pilih ISO Arch Linux
- enter

---

# 🌐 Connect WiFi

Kalau pake LAN skip bagian ini.

Masuk WiFi setup:

```bash
iwctl
```

Lihat device:

```bash
device list
```

Scan WiFi:

```bash
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

Kalau muncul reply berarti aman ✅

---

# 🚀 Mulai Install Arch

Jalankan:

```bash
archinstall
```

---

# ⚙️ Setting Archinstall

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

---

# 💽 Disk Configuration

Pilih:

```txt
Use best-effort default partition layout
```

---

# ⚠️ IMPORTANT DUAL BOOT

JANGAN pilih disk Windows utama kalau ada data penting.

Pilih:
- partisi kosong hasil shrink tadi

atau:

```txt
Free Space
```

---

# 🧱 Filesystem

Pilih:

```txt
ext4
```

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

Buat user:

| Setting | Contoh |
|---|---|
| Username | marcel |
| Password | bebas |

Centang:

```txt
Use sudo
```

---

# 🌐 Network

Pilih:

```txt
Use NetworkManager
```

---

# 🖼️ Desktop Environment

Pilih sesuai kebutuhan.

Contoh:
- Hyprland
- KDE Plasma
- GNOME
- XFCE

---

# 🔊 Audio

Pilih:

```txt
pipewire
```

---

# 📦 Kernel

Pilih:

```txt
linux
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

Ketik:

```bash
reboot
```

Lalu:
- cabut flashdisk

---

# ✅ Hasil Akhir

Saat nyala akan muncul:

```txt
GRUB
```

Isi:
- Arch Linux
- Windows Boot Manager

Dual boot berhasil 🎉
