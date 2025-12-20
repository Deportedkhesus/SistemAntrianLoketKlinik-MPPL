# 🎯 Panduan Operator Antrian

Dokumentasi lengkap untuk menggunakan **Panel Operator Antrian** dengan efisien.

---

## 🚀 Fitur-Fitur Operator Panel

### 1. **Status Panel - 2 Mode**

#### 🔵 Mode IDLE (Siap Memanggil)

```
┌─────────────────────────────────────┐
│ 🔵 SIAP MEMANGGIL         [Idle]   │
├─────────────────────────────────────┤
│  Tidak ada antrian sedang dilayani  │
│                                     │
│  Ada 5 antrian menunggu untuk      │
│  Poli Umum                          │
│                                     │
│  [📞 PANGGIL ANTRIAN (5 Menunggu)] │
└─────────────────────────────────────┘
```

**Karakteristik:**

- Border biru
- Badge "Idle" biru
- Tombol "PANGGIL ANTRIAN" aktif (jika ada antrian)
- Menampilkan jumlah antrian menunggu
- Disable jika tidak ada antrian

#### 🟠 Mode SERVING (Sedang Melayani)

```
┌─────────────────────────────────────┐
│ 🟠 SEDANG MELAYANI      [Proses]   │
├─────────────────────────────────────┤
│     Nomor Antrian Sedang Dilayani   │
│                                     │
│           🟠  A-004                 │
│         Sedang Dilayani             │
│                                     │
│ [✅ SELESAIKAN PELAYANAN]           │
│ [⚡ Selesai & Panggil Berikutnya]   │
│ [🔄 Panggil Ulang] [❌ Lewati]      │
└─────────────────────────────────────┘
```

**Karakteristik:**

- Border orange, background orange terang
- Badge "Proses" orange
- Nomor antrian besar (text-7xl) warna orange
- Tombol "SELESAIKAN PELAYANAN" hijau besar (h-14)
- Tombol sekunder lebih kecil

---

## 🎮 Tombol-Tombol Operator

### Tombol Utama (Primary Actions)

#### 1. ✅ **SELESAIKAN PELAYANAN** (Hijau Besar)

- **Kapan:** Saat sedang melayani pasien
- **Fungsi:**
    - Menandai pelayanan selesai
    - Status ticket → `done`
    - Kembali ke mode IDLE
    - Jika "Auto Panggil" aktif → otomatis panggil berikutnya setelah 1.5 detik
- **Shortcut:** Tombol ini muncul paling atas, ukuran besar
- **Warna:** `bg-green-600` tinggi `h-14`

#### 2. ⚡ **Selesai & Panggil Berikutnya** (Biru)

- **Kapan:** Saat sedang melayani + "Auto Panggil" OFF
- **Fungsi:**
    - Selesaikan pelayanan saat ini
    - Langsung panggil antrian berikutnya (1.5 detik delay)
    - Lebih cepat dari finish manual
- **Use Case:** Operator sibuk, ingin workflow cepat
- **Warna:** `bg-blue-600` tinggi `h-12`

#### 3. 📞 **PANGGIL ANTRIAN** (Biru Besar)

- **Kapan:** Mode IDLE + ada antrian menunggu
- **Fungsi:**
    - Memanggil antrian berikutnya dari queue
    - Play sound: "DING DING... Nomor antrian A 5..."
    - Status ticket → `called`
    - Update counter_id
    - Pindah ke mode SERVING
- **Label Dinamis:**
    - "PANGGIL ANTRIAN (5 Menunggu)" → jika ada 5 antrian
    - "Tidak Ada Antrian" → jika queue kosong (disabled)
- **Warna:** `bg-blue-600` tinggi `h-14`

### Tombol Sekunder (Secondary Actions)

#### 4. 🔄 **Panggil Ulang** (Outline Biru)

- **Kapan:** Saat sedang melayani
- **Fungsi:**
    - Play ulang sound announcement
    - Tidak mengubah status
    - Tidak memanggil ticket baru
- **Use Case:**
    - Pasien belum datang/tidak dengar
    - Pasien di toilet
    - Perlu reminder
- **Disabled:** Jika tidak ada ticket sedang dilayani
- **Warna:** `border-blue-300 text-blue-600`

#### 5. ❌ **Lewati Antrian** (Outline Orange)

- **Kapan:** Saat sedang melayani
- **Fungsi:**
    - Konfirmasi: "Apakah Anda yakin?"
    - Finish ticket saat ini (skip)
    - Otomatis panggil berikutnya setelah 1 detik
    - Notifikasi: "Antrian X dilewati" (warning)
- **Use Case:**
    - Pasien tidak datang dalam waktu lama
    - Emergency, perlu skip
    - Pasien pindah counter lain
- **Warning:** Jarang digunakan, hati-hati
- **Warna:** `border-orange-300 text-orange-600`

---

## ⚙️ Pengaturan

### 🔊 Pengaturan Suara

```
┌──────────────────────────────────┐
│ 🔊 Pengaturan Suara             │
├──────────────────────────────────┤
│ Status: ✅ Suara Aktif          │
│                                  │
│ Volume: ━━━━━━●━━━ 70%          │
│                                  │
│ [▶️ Test Suara]                  │
└──────────────────────────────────┘
```

- **Toggle Sound:** Tombol Volume2/VolumeX di header (kanan atas)
- **Volume Slider:** 0-100%, real-time adjustment
- **Test Suara:** Play "Test suara sistem antrian berhasil"
- **Persistence:** Disimpan di localStorage

### ⚡ Pengaturan Otomatis

```
┌──────────────────────────────────┐
│ ⚡ Pengaturan Otomatis          │
├──────────────────────────────────┤
│ Panggil Otomatis Setelah Selesai│
│ [Switch: ON/OFF]                 │
│                                  │
│ Otomatis memanggil berikutnya   │
│ setelah selesai melayani         │
└──────────────────────────────────┘
```

**Auto Call Next:**

- **ON:** Setelah finish → auto panggil next (1.5s delay)
- **OFF:** Tombol "Selesai & Panggil Berikutnya" muncul
- **Persistence:** Disimpan di localStorage (`autoCallNext`)

---

## 📊 Statistik Counter

### Card 1: Menunggu (Biru)

```
┌──────────────────┐
│ 🕐 Menunggu     │
│      5          │
│ Antrian menunggu│
└──────────────────┘
```

- Jumlah antrian menunggu untuk **layanan ini**
- Diambil dari `data.services[x].next.length`

### Card 2: Sedang Dilayani (Orange)

```
┌──────────────────┐
│ 👥 Sedang Dilayani│
│      1          │
│ Counter ini     │
└──────────────────┘
```

- **1** jika ada currentTicket (mode SERVING)
- **0** jika tidak ada (mode IDLE)

### Card 3: Selesai Hari Ini (Hijau)

```
┌──────────────────┐
│ ✅ Selesai Hari Ini│
│      0          │
│ Total dilayani  │
└──────────────────┘
```

- Total ticket `done` hari ini (TODO: implement count)

---

## 📋 Daftar Antrian Berikutnya

```
┌─────────────────────────────────────────┐
│ Daftar Antrian Berikutnya    [5 Menunggu]│
│ Antrian untuk layanan Poli Umum         │
├─────────────────────────────────────────┤
│ [1] A-005           [Berikutnya] 🔵      │
│ [2] A-006           [Menunggu]          │
│ [3] A-007           [Menunggu]          │
│ [4] A-008           [Menunggu]          │
│ [5] A-009           [Menunggu]          │
└─────────────────────────────────────────┘
```

**Fitur:**

- Nomor urut 1-10 (max 10 antrian ditampilkan)
- **Baris pertama** highlight biru (antrian berikutnya)
- Badge "Berikutnya" vs "Menunggu"
- Auto-refresh setiap 10 detik
- Empty state jika tidak ada antrian

---

## 🎬 Workflow Operator - Skenario

### Scenario A: Normal Flow (Auto Call OFF)

```
1. Pilih Counter → "Loket 1 - Poli Umum"
2. Status: IDLE, Ada 5 antrian menunggu
3. Klik "PANGGIL ANTRIAN (5 Menunggu)"
   → Sound: "DING DING... Nomor A-5..."
   → Status: SERVING, A-005 tampil besar
4. Melayani pasien A-005
5. Klik "SELESAIKAN PELAYANAN"
   → Status: IDLE
6. Klik "PANGGIL ANTRIAN (4 Menunggu)"
   → A-006 dipanggil
7. Repeat...
```

### Scenario B: Quick Flow (Auto Call ON)

```
1. Pilih Counter
2. Aktifkan "Auto Call Next" di settings
3. Klik "PANGGIL ANTRIAN"
   → A-005 dipanggil
4. Melayani pasien
5. Klik "SELESAIKAN PELAYANAN"
   → Otomatis panggil A-006 (1.5s delay)
6. Melayani A-006
7. Klik "SELESAIKAN PELAYANAN"
   → Otomatis panggil A-007
8. Repeat... (lebih cepat!)
```

### Scenario C: Express Flow (Finish + Call Next)

```
1. Pilih Counter
2. Auto Call: OFF
3. Klik "PANGGIL ANTRIAN" → A-005
4. Melayani pasien
5. Klik "Selesai & Panggil Berikutnya"
   → A-005 finish + A-006 langsung dipanggil
6. Repeat... (tercepat!)
```

### Scenario D: Pasien Tidak Datang

```
1. Status: SERVING, A-005 sedang dilayani
2. Pasien tidak datang setelah dipanggil
3. Klik "Panggil Ulang"
   → Sound play lagi
4. Tunggu 30 detik...
5. Masih tidak datang
6. Klik "Lewati Antrian"
   → Konfirmasi: OK
   → A-005 finish, A-006 dipanggil otomatis
```

### Scenario E: Pasien Di Toilet

```
1. Status: SERVING, A-005
2. Pasien bilang: "Sebentar ke toilet"
3. Klik "Panggil Ulang" beberapa kali
   → Play sound untuk reminder
4. Pasien kembali
5. Melayani
6. Klik "SELESAIKAN PELAYANAN"
```

---

## 🎨 Visual States

### State 1: IDLE + Ada Antrian

- **Border:** Blue (`border-blue-500`)
- **Badge:** "Idle" blue
- **Icon:** Phone blue
- **Button:** "PANGGIL ANTRIAN" blue, size lg (h-14)
- **Text:** "{X} antrian menunggu untuk {Service}"

### State 2: IDLE + Tidak Ada Antrian

- **Border:** Blue
- **Badge:** "Idle" blue
- **Icon:** Phone gray
- **Button:** "Tidak Ada Antrian" disabled
- **Text:** "Tidak ada antrian menunggu saat ini"

### State 3: SERVING

- **Border:** Orange (`border-orange-500`)
- **Background:** Orange light (`bg-orange-50`)
- **Badge:** "Proses" orange
- **Icon:** StopCircle orange (animate-pulse)
- **Ticket Display:** Border dashed orange, text-7xl orange
- **Button:** "SELESAIKAN PELAYANAN" green, large
- **Secondary Buttons:** Active (not disabled)

---

## 🔔 Notifikasi

### Success (Green)

- ✅ "Memanggil antrian A-005"
- ✅ "Pelayanan A-005 selesai"

### Info (Blue)

- ℹ️ "Memanggil ulang antrian A-005"
- ℹ️ "Test suara diputar"

### Warning (Orange)

- ⚠️ "Pilih counter terlebih dahulu"
- ⚠️ "Selesaikan pelayanan saat ini terlebih dahulu"
- ⚠️ "Antrian A-005 dilewati"

### Error (Red)

- ❌ "Gagal memanggil antrian"
- ❌ "Gagal menyelesaikan pelayanan"
- ❌ "Gagal melewati antrian"

**Duration:** 3 detik, auto-hide

---

## 🎯 Tips & Best Practices

### ✅ DO (Yang Harus Dilakukan)

1. ✅ Pilih counter dulu sebelum mulai
2. ✅ Test sound sebelum mulai shift
3. ✅ Gunakan "Auto Call Next" untuk busy hours
4. ✅ Gunakan "Panggil Ulang" jika pasien tidak dengar
5. ✅ Pastikan volume cukup keras (70-80%)
6. ✅ Monitor daftar antrian (ada berapa menunggu)

### ❌ DON'T (Yang Jangan Dilakukan)

1. ❌ Jangan klik "Panggil" saat masih melayani
2. ❌ Jangan "Lewati" antrian tanpa alasan kuat
3. ❌ Jangan lupa selesaikan pelayanan
4. ❌ Jangan matikan sound saat operasional
5. ❌ Jangan panggil ulang terlalu sering (spam)

### 💡 Pro Tips

1. **Busy Hours:** Aktifkan "Auto Call Next" untuk throughput maksimal
2. **Normal Hours:** Matikan "Auto Call" untuk kontrol lebih baik
3. **First Call:** Gunakan "Test Suara" untuk cek sistem
4. **Patient Missing:** Tunggu 30-60 detik sebelum "Lewati"
5. **Emergency:** Gunakan "Lewati" jika ada situasi urgent
6. **Sound Issue:** Cek browser permission + system volume

---

## 🐛 Troubleshooting

### Issue: Sound tidak bunyi

**Fix:**

1. Cek toggle sound (header kanan atas) → harus hijau
2. Klik "Test Suara" → dengar bunyi?
3. Cek volume slider → minimal 50%
4. Cek browser permission → allow audio
5. Cek system volume → tidak mute
6. Refresh page → coba lagi

### Issue: Tombol disabled/tidak bisa klik

**Fix:**

1. **"PANGGIL ANTRIAN" disabled:**
    - Cek apakah ada antrian menunggu
    - Cek apakah sudah pilih counter
    - Lihat badge: "{X} Menunggu" harus > 0

2. **"SELESAIKAN" tidak muncul:**
    - Pastikan ada currentTicket (mode SERVING)
    - Cek status: harus "Sedang Melayani"

3. **"Panggil Ulang" disabled:**
    - Harus dalam mode SERVING
    - Harus ada ticket sedang dilayani

### Issue: Data tidak update

**Fix:**

1. Refresh page (F5)
2. Cek koneksi internet
3. Cek backend server (Laravel)
4. Lihat console error (F12)

### Issue: Statistik salah

**Fix:**

- Statistik per-counter, bukan global
- "Menunggu" = antrian untuk service ini
- "Dilayani" = 1 jika ada currentTicket, 0 jika idle
- Jika masih salah → refresh

---

## 🚀 Quick Reference Card

```
┌────────────────────────────────────────────────────┐
│          OPERATOR CHEAT SHEET                      │
├────────────────────────────────────────────────────┤
│ 🔵 IDLE STATE                                      │
│   📞 PANGGIL ANTRIAN → Memanggil berikutnya       │
│                                                    │
│ 🟠 SERVING STATE                                   │
│   ✅ SELESAIKAN → Finish (+ auto next jika ON)    │
│   ⚡ SELESAI & NEXT → Finish + panggil langsung   │
│   🔄 PANGGIL ULANG → Play sound lagi             │
│   ❌ LEWATI → Skip + panggil next                │
│                                                    │
│ ⚙️ SETTINGS                                       │
│   🔊 Sound Toggle → ON/OFF                        │
│   🎚️ Volume → 0-100%                             │
│   ▶️ Test Suara → Cek audio                      │
│   ⚡ Auto Call → Auto/Manual                      │
│                                                    │
│ 🎯 SHORTCUTS                                      │
│   Quick Mode: Auto Call ON                        │
│   Express Mode: Selesai & Next Button            │
│   Normal Mode: Auto Call OFF                      │
└────────────────────────────────────────────────────┘
```

---

**Versi:** 2.0  
**Last Update:** 19 Oktober 2025  
**Author:** Gudang App Team
