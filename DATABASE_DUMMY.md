# 📊 Database Dummy Data Summary

Database telah di-reset dan diisi dengan data dummy yang lebih lengkap.

## 🔑 Users (3 users)

| Email                   | Password | Role               |
| ----------------------- | -------- | ------------------ |
| admin@puskesmas.com     | password | Admin              |
| operator1@puskesmas.com | password | Operator Poli Umum |
| operator2@puskesmas.com | password | Operator Poli Gigi |

## 🏥 Services (5 layanan)

| Code         | Name                              | Prefix | Status |
| ------------ | --------------------------------- | ------ | ------ |
| POLI-UMUM    | Poli Umum                         | A      | Active |
| POLI-GIGI    | Poli Gigi                         | B      | Active |
| FARMASI      | Farmasi                           | C      | Active |
| POLI-KIA     | Poli KIA (Kesehatan Ibu dan Anak) | D      | Active |
| LABORATORIUM | Laboratorium                      | E      | Active |

## 🪟 Counters (7 loket)

| ID  | Name                | Service      | Status |
| --- | ------------------- | ------------ | ------ |
| 1   | Loket 1 - Poli Umum | Poli Umum    | Active |
| 2   | Loket 2 - Poli Umum | Poli Umum    | Active |
| 3   | Loket Poli Gigi     | Poli Gigi    | Active |
| 4   | Loket Farmasi 1     | Farmasi      | Active |
| 5   | Loket Farmasi 2     | Farmasi      | Active |
| 6   | Loket KIA           | Poli KIA     | Active |
| 7   | Loket Laboratorium  | Laboratorium | Active |

## 🎟️ Tickets (32 tiket dummy)

### Poli Umum (A series) - 9 tickets

```
✅ A-001 (done)    - Dilayani di Loket 1, selesai 1 jam 45 menit lalu
✅ A-002 (done)    - Dilayani di Loket 2, selesai 1 jam 30 menit lalu
✅ A-003 (done)    - Dilayani di Loket 1, selesai 1 jam 10 menit lalu
🔵 A-004 (called)  - SEDANG dilayani di Loket 1 (5 menit lalu)
⏳ A-005 (waiting) - Menunggu
⏳ A-006 (waiting) - Menunggu
⏳ A-007 (waiting) - Menunggu
⏳ A-008 (waiting) - Menunggu
⏳ A-009 (waiting) - Menunggu
```

### Poli Gigi (B series) - 4 tickets

```
🔵 B-001 (called)  - SEDANG dilayani di Loket Poli Gigi (10 menit lalu)
⏳ B-002 (waiting) - Menunggu
⏳ B-003 (waiting) - Menunggu
⏳ B-004 (waiting) - Menunggu
```

### Farmasi (C series) - 10 tickets

```
🔵 C-001 (called)  - SEDANG dilayani di Loket Farmasi 1 (3 menit lalu)
🔵 C-002 (called)  - SEDANG dilayani di Loket Farmasi 2 (2 menit lalu)
⏳ C-003 (waiting) - Menunggu
⏳ C-004 (waiting) - Menunggu
⏳ C-005 (waiting) - Menunggu
⏳ C-006 (waiting) - Menunggu
⏳ C-007 (waiting) - Menunggu
⏳ C-008 (waiting) - Menunggu
⏳ C-009 (waiting) - Menunggu
⏳ C-010 (waiting) - Menunggu
```

### Poli KIA (D series) - 2 tickets

```
⏳ D-001 (waiting) - Menunggu
⏳ D-002 (waiting) - Menunggu
```

### Laboratorium (E series) - 5 tickets

```
🔵 E-001 (called)  - SEDANG dilayani di Loket Laboratorium (8 menit lalu)
⏳ E-002 (waiting) - Menunggu
⏳ E-003 (waiting) - Menunggu
⏳ E-004 (waiting) - Menunggu
⏳ E-005 (waiting) - Menunggu
```

## 📈 Statistics Summary

- **Total Tickets**: 32
- **Sedang Dilayani** (called): 4 tickets
    - A-004 di Loket 1
    - B-001 di Loket Poli Gigi
    - C-001 di Loket Farmasi 1
    - C-002 di Loket Farmasi 2
    - E-001 di Loket Laboratorium
- **Menunggu** (waiting): 25 tickets
- **Selesai** (done): 3 tickets

## 🧪 Testing Scenarios

### 1. Test Display Screen (`/queue/display`)

- Buka di browser, akan tampil 4 layanan sedang dipanggil
- Sound system akan announce nomor yang dipanggil (jika autoplay diizinkan)

### 2. Test Ticket Generation (`/queue/ticket`)

- Pilih layanan (contoh: Poli Umum)
- Klik generate ticket
- Akan muncul nomor antrian baru (A-010 jika Poli Umum)

### 3. Test Management Panel (`/queue/management`)

#### Scenario A: Melayani Antrian yang Sudah Ada

1. Login sebagai operator1@puskesmas.com
2. Pilih Counter: "Loket 1 - Poli Umum"
3. Akan tampil A-004 sedang dilayani (status ORANGE)
4. Klik "SELESAIKAN PELAYANAN" (tombol hijau besar)
5. Status akan kembali ke IDLE (biru)
6. Klik "Panggil Berikutnya" untuk memanggil A-005

#### Scenario B: Memulai dari Counter Idle

1. Pilih Counter: "Loket 2 - Poli Umum"
2. Tidak ada antrian sedang dilayani (status IDLE)
3. Klik "Panggil Berikutnya"
4. A-005 akan dipanggil (status berubah ORANGE)
5. Sound akan berbunyi: "DING DING... Nomor antrian A 5, silakan ke Loket 2 Poli Umum"
6. Setelah selesai melayani, klik "SELESAIKAN PELAYANAN"

#### Scenario C: Panggil Ulang

1. Saat ada ticket sedang dilayani (status ORANGE)
2. Klik "Panggil Ulang"
3. Sound akan berbunyi lagi dengan nomor yang sama

#### Scenario D: Test Sound

1. Klik tombol "Test Suara"
2. Sound akan berbunyi: "DING DING... Test suara sistem antrian berhasil"
3. Gunakan slider volume untuk adjust volume (0-100%)

### 4. Test Statistics Accuracy

- **Loket 1**: Akan show 1 sedang dilayani (A-004), bukan 4
- **Loket 2**: Akan show 0 sedang dilayani
- **Farmasi**: Kedua loket masing-masing show 1 sedang dilayani

## 🔄 Reset Database

Untuk reset ulang database dengan data dummy ini:

```bash
php artisan migrate:fresh --seed
```

## ⚠️ Notes

1. **Password semua user**: `password`
2. **Timestamp relatif**: Beberapa ticket menggunakan timestamp relatif (subMinutes, subHours) agar terlihat realistic
3. **Status ticket**:
    - `waiting`: Belum dipanggil, masih menunggu
    - `called`: Sedang dipanggil/dilayani di counter
    - `done`: Sudah selesai dilayani
    - `cancelled`: Dibatalkan (tidak ada di dummy data)
4. **Sound delay**: 300ms delay ditambahkan untuk comply dengan browser autoplay policy
5. **Workflow enforcement**: Tidak bisa panggil ticket berikutnya saat masih ada yang sedang dilayani
