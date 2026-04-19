# tugas-mobile
---
### 1. [Materi 11](./materi11.md)
### 1. [Materi 12](./materi12.md)
### 1. [Materi API](./materi12.md)

\
\

---
# Sedikit tutorial menjalankan project di HP android

---

### 1. Aktifkan Developer Mode & USB Debugging di HP

* Masuk ke **Settings > About Phone**
* Tekan **Build Number** ±7 kali sampai muncul *Developer Options*
* Masuk ke **Developer Options**

  * Aktifkan **USB Debugging**
  * (Opsional tapi penting) aktifkan **Install via USB**

---

### 2. Hubungkan HP ke Laptop pakai USB

* Gunakan kabel data (bukan cuma charging)
* Di HP akan muncul popup:

  > **Allow USB Debugging?** → klik **Allow**
* Centang *Always allow* biar gak ditanya lagi

---

### 3. Cek apakah device terbaca

Di terminal / CMD:

```bash
flutter devices
```

Kalau berhasil, akan muncul list device, contoh:

```
2 connected devices:

Redmi Note 10 (mobile) • 192.168.1.5:5555 • android-arm64 • Android 12
```

atau:

```
Redmi Note 10 • 1234567890 • android-arm64 • Android 12
```

👉 **Yang penting adalah DEVICE ID-nya** (contoh: `1234567890`)

---

### ❗ Kalau device tidak muncul

Coba ini:

```bash
adb devices
```

Kalau statusnya:

* `unauthorized` → cek HP, klik Allow
* kosong → kemungkinan:

  * kabel jelek
  * driver belum kebaca
  * USB mode belum ke **File Transfer (MTP)**

Restart adb:

```bash
adb kill-server
adb start-server
```

---

###  4. Masuk ke project Flutter

```bash
cd nama_project_flutter
```

---

###  5. Jalankan ke device langsung

```
Redmi Note 10 • 1234567890 • android-arm64 • Android 12
```

👉 **Yang penting adalah DEVICE ID-nya** (contoh: `1234567890`)

Gunakan:

```bash
flutter run -d <device-id>
```

Contoh:

```bash
flutter run -d 1234567890
```

---
