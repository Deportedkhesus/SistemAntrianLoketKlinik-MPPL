
LAPORAN TUGAS MANAJEMEN PROYEK PERANGKAT LUNAK UJIAN TENGAH SEMESTER GANJIL TAHUN AKADEMIK 2025/2026 
 Sistem Antrian Loket Klinik (SALK)


 

Dibuat Oleh : 
M Dantha Arianvasya 			1237050106
Muhamad Khansa Khalifaturohman 	1247050115
Hilman Maulana				1237050020
Idha Hamidaturrosadi			1237050026
Hasna Minatul Mardiah			1237050024
Irsyad Adfiansha Hidayat		1237050042
Lutfi Nurhidayat				1237050123
Hafizultan Fanzaulid			1237050097
Firman Adi Nugraha			1237050016


UNIVERSITAS ISLAM NEGERI SUNAN GUNUNG DJATI BANDUNG
FAKULTAS SAINS DAN TEKNOLOGI
JURUSAN TEKNIK INFORMATIKA
TAHUN AJARAN 2025

BAB 1
1.1. Latar Belakang Masalah 
Pelayanan farmasi merupakan komponen vital dalam sistem layanan kesehatan, khususnya di lingkungan klinik. Di tahap ini, pasien memperoleh obat sebagai bagian dari penanganan medis, sehingga kecepatan, ketertiban, dan akurasi pelayanan sangat menentukan kualitas pengalaman pasien secara keseluruhan. Namun, realitas di lapangan menunjukkan bahwa banyak klinik masih mengandalkan sistem antrean manual untuk memanggil pasien ke loket farmasi. Pemanggilan dilakukan secara lisan oleh petugas, sementara pencatatan nomor antrean dilakukan secara tertulis atau tidak terstruktur. Kondisi tersebut sering kali menimbulkan sejumlah kendala, seperti ketidakteraturan antrean, kesalahan dalam pemanggilan, serta ketidaknyamanan bagi pasien yang menunggu tanpa kepastian informasi antrean.
Seiring dengan berkembangnya teknologi informasi dan komunikasi, digitalisasi layanan kesehatan menjadi langkah strategis untuk meningkatkan efisiensi dan akurasi pelayanan. Salah satu bentuk implementasinya adalah melalui sistem antrean digital berbasis web yang mampu mengotomatisasi proses pengambilan nomor, menampilkan status antrean secara real-time, dan memberikan kemudahan bagi petugas dalam mengelola alur pelayanan. Dengan adanya sistem seperti ini, diharapkan proses antrean menjadi lebih teratur, transparan, dan mudah diakses, baik oleh pasien maupun oleh tenaga kesehatan yang bertugas.
Sebagai respons terhadap permasalahan tersebut, dirancanglah Sistem Antrean Loket Klinik (SALK), yaitu sebuah aplikasi antrean digital berbasis web yang ditujukan untuk mempermudah proses pengambilan dan pemanggilan antrean di loket farmasi. Sistem ini memungkinkan pasien untuk mengambil nomor antrean secara mandiri, memantau status antrean secara daring, serta memungkinkan petugas dan admin untuk mengelola antrean melalui dashboard yang terintegrasi. Proyek ini tidak hanya dirancang sebagai solusi terhadap permasalahan operasional di klinik, tetapi juga sebagai media pembelajaran berbasis proyek (project-based learning) bagi mahasiswa dalam mengembangkan perangkat lunak yang sesuai dengan kebutuhan pengguna nyata, dengan melibatkan proses analisis, desain antarmuka, pengembangan sistem, pengujian, hingga manajemen tim pengembang.
Dengan demikian, pengembangan SALK diharapkan mampu memberikan kontribusi nyata dalam peningkatan mutu layanan farmasi di klinik serta memperkuat kompetensi mahasiswa dalam merancang solusi digital yang aplikatif dan berdampak langsung.

1.2. Rencana Proyek 
Proyek ini merupakan pengembangan Sistem Antrean Loket Klinik (SALK), yaitu sebuah website untuk mempermudah pasien dalam mengambil nomor antrean di loket Poli Klinik, sekaligus membantu petugas dan admin dalam mengelola antrean secara efisien. Sistem ini akan menjadi solusi digital yang mendukung pelayanan agar lebih cepat, transparan, dan nyaman bagi semua pihak.
1.2.1 Tujuan Proyek
Membuat sistem antrean digital yang mempersingkat waktu tunggu pasien dalam mengambil obat.
Menyediakan tampilan display antrean real-time yang dapat diakses oleh pasien maupun petugas loket.
Menyediakan dashboard petugas untuk mengelola antrean (memanggil pasien, menandai status antrean, melihat riwayat).
Menyediakan modul admin untuk manajemen, konfigurasi tampilan, serta laporan aktivitas.
Menjadi proyek pembelajaran mahasiswa yang mengintegrasikan analisis kebutuhan, perancangan UI/UX, serta implementasi frontend–backend.
1.2.2 Lingkup Proyek
Modul Antrean Pasien: ambil tiket antrean online, lihat status antrean, dan display antrean.
Modul Dashboard Petugas: login, kelola antrean aktif, riwayat antrean, reset harian.
Modul Admin: manajemen petugas, manajemen display antrean, laporan aktivitas.
Kebutuhan Non-Fungsional: responsif, performa cepat (<2 detik), keamanan data, ketersediaan selama jam operasional, dan kemudahan penggunaan.
1.2.3 Tim Proyek
Project Manager (1 orang): mengatur jalannya proyek dan koordinasi tim.
System Analyst (1 orang): memastikan kebutuhan sistem sesuai dengan tujuan.
UI/UX Designer (2 orang): merancang antarmuka dengan Figma.
Frontend Developer (2 orang): membangun antarmuka dengan React.js.
Backend Developer (2 orang): mengembangkan API dan logika server dengan PHP dan SQLite.
Quality Assurance (1 orang): melakukan uji sistem agar sesuai dengan kebutuhan.
1.2.4 Teknologi yang Digunakan
Frontend: React.js
Backend: PHP
Database: SQLite
Desain UI/UX: Figma
1.2.5 Hasil yang Diharapkan
Website fungsional untuk pasien, petugas, dan admin.
Tampilan dashboard dan display antrean real-time.
Laporan aktivitas harian untuk mendukung evaluasi pelayanan.
Produk akhir dapat digunakan secara nyata serta menjadi portofolio pembelajaran tim pengembang.
1.3. Rencana Pembiayaan Proyek

No
Komponen
Rincian / Keterangan
Estimasi Bulanan (Rp)
Estimasi Tahunan (Rp)
1
Hosting Website
Layanan hosting backend & frontend (Railway, Vercel, atau Hostinger)
50.000
600.000
2
Domain
Nama domain website (contoh: salkclinic.my.id atau .com)
12.500
150.000
3
Database Server (SQLite/MySQL Cloud)
Penyimpanan data antrean pasien dan petugas
30.000
360.000
4
Storage & Backup Cloud
Cadangan data antrean dan log aktivitas
25.000
300.000
5
Sertifikat SSL & Keamanan
Keamanan koneksi HTTPS (Let’s Encrypt / alternatif berbayar)
10.000
120.000
6
Desain UI/UX (Figma Pro)
Lisensi kolaboratif untuk 2 desainer UI/UX
16.500
200.000
7
Subtotal Infrastruktur Software


144.000
1.730.000

Tabel 1. Rencana Pembiayaan Proyek.


1.4. Rencana Penjadwalan Proyek

Nama
Status
Durasi Waktu
Penentuan Posisi Developer dan Pembagian Tugas
 Approved
1 – 7 September 2025
Sprint 1 – Perancangan & Desain Sistem
 Approved
8 – 28 September 2025
Sprint 2 – Pengembangan Fitur Utama (Frontend & Backend)
 In progress
29 September – 26 Oktober 2025
Sprint 3 – Integrasi & Penyempurnaan Fitur
 Not started
27 Oktober – 30 November 2025
Website Testing (Uji Coba Sistem)
 Not started
1 – 14 Desember 2025
Deploy Website & Evaluasi Akhir
 Not started
15 – 28 Desember 2025

Tabel 2. Rencana Penjadwalan Proyek.






























BAB II LANDASAN TEORI 
2.1 Teori Sistem Antrean Loket Klinik (SALK)
Sistem Antrean Loket Klinik (SALK) merupakan sistem berbasis web yang dikembangkan untuk mengelola proses pengambilan nomor antrean dan pelayanan resep obat di loket farmasi secara digital, teratur, dan real-time. Penerapan sistem ini didasari oleh beberapa teori utama yang saling berkaitan, yaitu teori antrean, teori interaksi manusia dan komputer (HCI), dan teori sistem informasi.
2.1.1 Teori Antrean (Queuing Theory)
Teori antrean merupakan cabang penelitian operasi (operational research) yang digunakan untuk menganalisis hubungan antara kapasitas layanan, jumlah petugas, dan waktu tunggu pasien dalam suatu sistem pelayanan. Adeoye et al. (2021) menjelaskan bahwa penerapan teori antrean di lingkungan farmasi mampu memprediksi dan mengoptimalkan waktu tunggu pasien dengan cara menyesuaikan jumlah petugas dan titik layanan agar beban kerja seimbang serta biaya operasional tetap efisien.
Temuan serupa juga diungkapkan oleh Bahadori et al. (2014), yang melalui simulasi sistem antrean di apotek rumah sakit menunjukkan bahwa peningkatan jumlah petugas pada tahap pengisian resep dapat menurunkan panjang antrean hingga 50% dan waktu tunggu pasien hingga 18 menit. Dengan menerapkan prinsip tersebut, SALK dirancang untuk mengatur antrean secara otomatis, memberikan estimasi waktu tunggu, serta menampilkan status pelayanan yang transparan bagi pasien dan petugas.
2.1.2 Teori Interaksi Manusia dan Komputer (Human–Computer Interaction)
Menurut Langote et al. (2024), Human–Computer Interaction (HCI) adalah disiplin ilmu yang mempelajari bagaimana sistem komputer dirancang agar dapat digunakan manusia secara efektif, efisien, dan menyenangkan, khususnya dalam konteks layanan kesehatan. Penerapan prinsip HCI pada SALK terlihat pada perancangan antarmuka yang responsif dan ramah pengguna, seperti tombol “Ambil Nomor Antrean” yang mudah diakses, umpan balik visual berupa nomor antrean dan estimasi waktu tunggu, serta tampilan dashboard interaktif untuk petugas.
Pendekatan user-centered design yang digunakan sejalan dengan rekomendasi Langote et al. (2024), di mana sistem kesehatan digital yang berorientasi pada kenyamanan pengguna terbukti mampu meningkatkan efisiensi kerja petugas serta mengurangi kesalahan dalam proses pelayanan.
2.1.3 Teori Sistem Informasi
Menurut Jogiyanto (2005), sistem informasi adalah kombinasi antara manusia, perangkat keras, perangkat lunak, jaringan komunikasi, dan prosedur yang dirancang untuk mengolah data menjadi informasi yang berguna bagi pengambilan keputusan. Dalam konteks SALK, teori ini menjadi dasar dalam perancangan arsitektur sistem yang mencakup tiga modul utama: modul pasien, modul petugas, dan modul admin.
Melalui pendekatan analisis dan desain terstruktur seperti yang dijelaskan oleh Jogiyanto, setiap komponen SALK dibangun berdasarkan kebutuhan fungsional yang jelas, mulai dari proses pengambilan nomor antrean, pengelolaan data antrean oleh petugas, hingga laporan aktivitas harian oleh admin, sehingga alur sistem menjadi terintegrasi, efisien, dan mudah dipelihara.

 
2.2 Metode Pengembangan Perangkat Lunak 
2.2.1 Metode Pengembangan
Dalam membuat sebuah aplikasi atau sistem, diperlukan langkah-langkah yang jelas agar proses pengerjaan bisa lebih terarah. Tanpa metode yang tepat, pengembangan bisa berjalan tidak teratur dan hasil akhirnya tidak sesuai kebutuhan. Oleh karena itu, pada pembuatan web loket antrian ini dipilih metode pengembangan Waterfall. Metode ini dianggap cocok karena alurnya runtut, mudah dipahami, dan sesuai untuk sistem yang kebutuhan dan fungsinya sudah jelas sejak awal.
2.2.2 Definisi Metode Waterfall
Metode Waterfall adalah model pengembangan perangkat lunak yang dikerjakan secara bertahap, dari satu langkah ke langkah berikutnya. Prosesnya menyerupai aliran air terjun: setelah satu tahap selesai, baru bisa lanjut ke tahap selanjutnya. Tahap-tahap ini meliputi analisis kebutuhan, desain, implementasi, pengujian, penerapan, hingga pemeliharaan. Karena sifatnya yang berurutan, metode ini memudahkan pengembang untuk mendokumentasikan setiap langkah dan menjaga agar sistem yang dibuat tetap sesuai dengan rencana. 
2.2.3 Tahapan Metode Waterfall
Metode Waterfall terdiri dari beberapa tahapan yang dilakukan secara berurutan. Setiap tahap memiliki keluaran (output) yang menjadi masukan (input) bagi tahap berikutnya. Diagram tahapan dari metode pengembangan Waterfall adalah sebagai berikut.

Gambar 1. Diagram Metode Pengembangan Waterfall.
Adapun tahapan dalam metode Waterfall adalah sebagai berikut.
a. Analisis Kebutuhan
Tahap pertama adalah analisis kebutuhan yang bertujuan untuk merumuskan fungsi-fungsi yang harus tersedia pada sistem. Analisis ini dibagi menjadi dua bagian, yaitu kebutuhan fungsional dan non-fungsional.
1. Kebutuhan Fungsional
Modul Antrian Pasien
Ambil Tiket Antrian: pengguna menekan tombol “Ambil Nomor Antrian” dan sistem akan menampilkan nomor antrian serta estimasi waktu tunggu.
Lihat Status Antrian: menampilkan nomor antrian aktif, nomor yang sedang dipanggil, dan estimasi waktu pelayanan.
Display Antrian: tampilan layar besar yang menunjukkan antrean saat ini, nomor berikutnya, serta status loket.
Modul Dashboard Petugas
Login Petugas: akses aman untuk masuk ke sistem.
Kelola Antrean: melihat daftar antrean aktif beserta statusnya (menunggu, dipanggil, selesai), serta fitur “Panggil Pasien” untuk menampilkan nomor di display antrian.
Riwayat Antrean: menampilkan daftar antrean yang sudah selesai.
Reset Harian: mengatur ulang antrean setiap hari.
Modul Admin
Manajemen Petugas: menambah, menghapus, dan memperbarui akun petugas.
Manajemen Display: mengatur konfigurasi tampilan antrean, termasuk warna, posisi teks, dan audio notifikasi.
Laporan Aktivitas: menampilkan data statistik antrean per hari, seperti jumlah pasien dan rata-rata waktu pelayanan.
1. Kebutuhan non-fungsional
Responsivitas: website dapat diakses melalui komputer loket maupun smartphone pasien.
Performa: sistem memproses pengambilan antrean dan pembaruan status dengan cepat (kurang dari 2 detik).
Keamanan Data: terdapat autentikasi untuk petugas dan admin, serta pembatasan akses data pasien.
Ketersediaan: sistem siap digunakan sepanjang jam operasional tanpa gangguan.
Kemudahan Penggunaan (Usability): antarmuka sederhana sehingga mudah dipahami oleh pasien maupun petugas.

b. Desain
Tahap ini bertujuan merancang sistem berdasarkan kebutuhan yang telah dikumpulkan. Desain mencakup perancangan database, arsitektur sistem, serta rancangan antarmuka pengguna. Pada tahap ini juga dibuat diagram seperti DFD (Data Flow Diagram), ERD (Entity Relationship Diagram), dan rancangan halaman web yang akan digunakan pada sistem loket antrian.
c. Implementasi
Setelah desain sistem selesai, tahap berikutnya adalah implementasi. Pada tahap ini, desain yang telah dibuat diwujudkan dalam bentuk kode program. Web loket antrian diimplementasikan menggunakan bahasa pemrograman PHP dengan database MySQL serta framework Bootstrap untuk membantu dalam tampilan antarmuka.
d. Pengujian
Pengujian dilakukan untuk memastikan bahwa sistem telah berjalan sesuai kebutuhan. Pengujian mencakup uji coba fungsional, seperti pengambilan nomor antrian, pemanggilan nomor antrian, serta pengujian tampilan laporan. Selain itu, dilakukan juga pengujian non-fungsional seperti kinerja dan kecepatan respon sistem.
e. Penerapan
Tahap penerapan dilakukan dengan memasang sistem yang sudah diuji pada lingkungan sebenarnya agar dapat digunakan oleh pengguna. Dalam konteks web loket antrian, tahap ini berarti sistem dipasang di server dan mulai digunakan di loket pelayanan.
f. Pemeliharaan
Tahap terakhir adalah pemeliharaan. Pada tahap ini dilakukan perbaikan jika ditemukan bug atau kesalahan, serta pengembangan lebih lanjut apabila ada penambahan fitur baru sesuai dengan kebutuhan pengguna di masa depan.
2.3 Alat dan Bahan Penelitian
Adapun alat dan bahan yang mendukung dalam perancangan dan penelitian ini adalah sebagai berikut.
2.3.1       Alat
        	Berikut adalah alat yang akan digunakan dalam penelitian ini.
1.     Hardware:
 Digunakan untuk menulis kode program, merancang antarmuka, serta menjalankan server lokal selama proses pengujian. Spesifikasi minimal yang digunakan dalam penelitian ini adalah:
Prosesor: Intel Core i5 atau setara


RAM: 8 GB


Penyimpanan: 256 GB SSD


Sistem Operasi: Windows 10 atau lebih baru

2. Perangkat Lunak (Software)
React.js: digunakan sebagai front-end framework untuk membangun tampilan antarmuka pengguna yang interaktif dan responsif.


Laravel (PHP Framework): digunakan sebagai back-end framework untuk mengatur logika bisnis, autentikasi, dan komunikasi dengan basis data.


SQLite: digunakan sebagai sistem manajemen basis data yang ringan dan terintegrasi dengan Laragon.


Laragon: digunakan sebagai lingkungan pengembangan lokal (local server) untuk menjalankan aplikasi Laravel dan basis data SQLite.


Visual Studio Code: digunakan sebagai code editor dalam penulisan dan pengelolaan proyek.


Google Chrome / Mozilla Firefox: digunakan untuk menguji antarmuka sistem secara langsung di peramban web.


Git & GitHub: digunakan untuk manajemen versi dan penyimpanan kode secara daring.


Hosting Provider: digunakan untuk penerapan (deployment) sistem agar dapat diakses secara online.
2.3.2       Bahan
Bahan penelitian yang digunakan berupa data simulasi pasien dan petugas yang digunakan untuk menguji sistem. Data ini meliputi:
Data Pasien, seperti nama, nomor antrean, dan waktu pelayanan.


Data Petugas, meliputi nama pengguna, kata sandi, serta hak akses ke dalam sistem.


Data Antrean Harian, digunakan untuk menguji fitur reset, laporan aktivitas, serta estimasi waktu tunggu.

2.4 Rancangan Sistem
Rancangan sistem merupakan tahap yang bertujuan untuk menggambarkan secara menyeluruh bagaimana sistem akan bekerja, mulai dari aliran data, struktur basis data, hingga tampilan antarmuka yang akan digunakan oleh pengguna. Tahap ini menjadi jembatan antara hasil analisis kebutuhan dan proses pengembangan sistem. Pada SALK (Sistem Antrian Loket Klinik), rancangan sistem meliputi pembuatan Diagram Konteks, Data Flow Diagram (DFD), Entity Relationship Diagram (ERD), serta rancangan antarmuka pengguna untuk admin dan petugas.
2.4.1 Data Flow Diagram (DFD
DFD Level 0
DFD Level 0, juga dikenal sebagai Context Diagram, memberikan gambaran umum aliran data antara sistem utama Sistem Manajemen Antrean Loket Klinik (SALK) dengan entitas eksternal yang berinteraksi. Diagram ini menunjukkan bagaimana SALK menerima, memproses, dan mengembalikan informasi ke Admin, Pegawai, dan User/Pasien, serta bagaimana sistem berinteraksi dengan data store internal (D1–D5).

Gambar 2.1 DFD Level 0












Tabel 2.1 Keterangan DFD Level 0
Nomor
Proses
Nama Proses
Masukkan
Keluaran
0
0.0
Sistem Manajemen Antrean Loket Klinik (SALK)
Entitas (Eksternal): Admin – data layanan (service), konfigurasi loket/counter, aktivasi/penonaktifan, pengaturan & prefix tiket, pembuatan akun pegawai. Pegawai – aksi panggil nomor, ubah status tiket (menunggu/dipanggil/selesai), input catatan pemanggilan. User/Pasien – permintaan ambil tiket, pilihan layanan (service/poli), cek status antrean. Data Store (Internal): D1: Users – data akun admin/pegawai dan (opsional) identitas pasien. D2: Services – daftar layanan/poli aktif, prefix, aturan kuota. D3: Counters – daftar loket/counter, status aktif, penugasan. D4: Tickets – tiket antrean, nomor, status, referensi service/counter. D5: Calls – riwayat pemanggilan tiket (waktu, counter, petugas).
Entitas (Eksternal): Admin – data master (services, counters), laporan ringkas antrean, log aktivitas, status sistem. Pegawai – daftar tiket aktif per layanan/counter, next number, konfirmasi panggilan sukses, ringkasan harian. User/Pasien – nomor tiket & estimasi panggilan, status antrean real-time, bukti/QR (opsional). Data Store (Internal): D1: Users – baca/tulis akun & otorisasi. D2: Services – baca/tulis perubahan layanan. D3: Counters – baca/tulis perubahan counter. D4: Tickets – simpan/ambil tiket & status. D5: Calls – simpan/ambil riwayat panggilan.


Input Informasi oleh Entitas
Admin
Menambahkan/mengubah Services (D2): nama poli, prefix tiket, kuota, aktif/non-aktif.
Mengelola Counters (D3): nama loket, status, penugasan pegawai.
Manajemen Users (D1): buat akun pegawai, memilih peran & akses loket.
Pegawai
Mengambil daftar tiket aktif per layanan/loket.
Mengubah status tiket (D4) dan mencatat pemanggilan (D5).
Menandai selesai/ulang panggilan.
User/Pasien
Memilih service/poli dan minta tiket.
Melakukan cek status antrean (posisi, nomor antrian).
Contoh Input
Pasien memilih Poli Umum ➜ sistem membuat Tiket baru (mis. A-023) pada D4 dan mengaitkannya dengan Service terkait di D2.


Pemrosesan Data oleh Sistem (SALK)
Validasi & otorisasi (D1: Users): pastikan peran Admin/Pegawai sesuai aksi.
Manajemen master data: CRUD layanan (D2) & counter (D3) sesuai aksi Admin.
Penerbitan tiket (D4: Tickets):
Menentukan prefix dan penomoran berikutnya berdasarkan Service aktif.
Menyimpan waktu ambil, status awal menunggu, dan (opsional) identitas ringkas.
Antrian & pemanggilan (D4 ↔ D5):
Menghitung next number per layanan/counter.
Saat Pegawai memanggil, sistem menandai tiket (dipanggil/selesai) di D4 dan merekam Calls di D5 (waktu, counter, petugas).
Estimasi & monitoring real-time
Menghitung posisi dan estimasi waktu panggilan bagi User/Pasien.
Menyediakan feed status untuk tampilan display.
Pelaporan ringkas:
Total tiket per layanan/counter, SLA panggilan rata-rata, log aktivitas pegawai.

Pemrosesan Data oleh Sistem (SALK)
Admin
Ringkasan & laporan: jumlah tiket per layanan, rata-rata waktu tunggu, aktivitas pegawai.
Status master data: daftar layanan/counter aktif, perubahan terbaru.
Pegawai
Daftar antrean per layanan/counter (waiting/next/ongoing).
Konfirmasi pemanggilan dan notifikasi jika tiket dipanggil.
Rekap harian (jumlah dilayani, durasi rata-rata).
User/Pasien
Nomor tiket (mis. A-023) dengan nomor loket (mis. Poli-Umum).
Status real-time: menunggu / dipanggil / selesai.

DFD Level 1
DFD Level 1 memecah proses utama SALK menjadi empat sub-proses: 1.0 Manajemen User, 2.0 Manajemen Layanan & Loket, 3.0 Manajemen Panggilan Tiket, dan 4.0 Manajemen Tiket. Setiap proses berinteraksi dengan entitas eksternal (Admin, Pegawai, User/Pasien) dan data store D1–D5: Users, Services, Counters, Tickets, Calls.

Gambar 2.2 DFD level 1

Tabel 2.2 Keterangan DFD Level 1
No
Proses
Nama Proses
Masukkan
Keluaran
1.0
–
Manajemen User
Admin: data akun & peran; permintaan aktivasi/non-aktif. Sistem: kredensial login/refresh token. D1: Users (baca/tulis)
Admin: konfirmasi buat/ubah/hapus user; status autentikasi. D1: Users: data user terbarui; catatan login.
2.0
–
Manajemen Layanan & Loket
Admin: definisi layanan (nama, prefix, kuota, aktif); konfigurasi loket (nama, status, penugasan). D2: Services, D3: Counters (baca/tulis)
Admin: daftar services & counters terbaru; notifikasi perubahan. D2, D3: data master tersimpan/terubah.
3.0
–
Manajemen Panggilan Tiket
Pegawai: aksi panggil berikutnya, ulang panggilan, tandai selesai. D4: Tickets (baca/tulis status), D5: Calls (tulis log)
Pegawai: nomor berikutnya, konfirmasi pemanggilan/penyelesaian; rekap harian. User/Pasien (display): status dipanggil / selesai. D4, D5: status tiket & log panggilan tersimpan.
4.0
–
Manajemen Tiket
User/Pasien: permintaan ambil tiket + pilihan layanan. Admin (opsional): pembatalan/penyesuaian. D2: Services (baca prefix & aturan), D4: Tickets (tulis)
User/Pasien: nomor tiket & estimasi; tautan/QR (opsional); status antrean. Admin: daftar tiket per layanan. D4: tiket baru/terperbarui.


Input Informasi oleh Entitas
Masukan
Data akun dari Admin: nama, email, role (administrator/admin/pegawai).
Permintaan aktivasi/non-aktif/ubah peran.
Kredensial login dari pengguna (admin/pegawai).
Pemrosesan
Validasi input & cek duplikasi email.
Hash password, set role & status.
CRUD pada D1: Users; rekam jejak login.
validasi token sesi.
Keluaran
Konfirmasi pembuatan/perubahan user ke Admin.
Status autentikasi (berhasil/gagal) ke peminta akses.
D1 terbarui (akun, role, status).
Contoh
Admin membuat akun pegawai baru; sistem menyimpan ke D1 dan menampilkan “Akun pegawai berhasil dibuat”.

Manajemen Layanan & Loket
Masukan
Dari Admin: tambah/ubah/hapus Service (nama, prefix, kuota, aktif); tambah/ubah Counter (nama, status).
Pemrosesan
Validasi unik prefix & nama layanan.
Sinkron kuota/aktif terhadap tiket berjalan (hindari konflik).
CRUD pada D2: Services dan D3: Counters.
Keluaran
Daftar layanan & loket terbaru ke Admin (3.0 & 4.0)
D2 dan D3 tersinkron.
Contoh
Admin menonaktifkan “Poli Gigi”; sistem menandai D2.services.is_active=false dan mencegah penerbitan tiket baru untuk layanan itu.
Manajemen Panggilan Tiket
Masukan
Pegawai menekan Panggil Berikutnya / Ulang PanggiI / Selesai.
Data tiket dari D4: Tickets; tulis log ke D5: Calls.
Pemrosesan
Hitung next number per layanan/counter (FIFO/prioritas).
Ubah status tiket: menunggu → dipanggil → selesai/batal.
Simpan catatan pemanggilan: waktu, counter, petugas di D5.
Trigger update ke display/antarmuka pasien.
Keluaran
Nomor tiket yang dipanggil & konfirmasi status ke Pegawai.
Update status real-time ke User/Pasien (display/monitor).
Rekap harian petugas (jumlah dilayani, durasi rata-rata).
D4 & D5 terbarui.
Contoh
Pegawai di Counter-2 memanggil tiket berikutnya: sistem mengubah T-102 jadi dipanggil di D4 dan menulis log ke D5.
Manajemen Tiket
Masukan
User/Pasien memilih layanan dan meminta tiket.
(Opsional) Admin membatalkan atau mengoreksi tiket tertentu.
Baca aturan prefix/kuota dari D2, tulis tiket ke D4.
Pemrosesan
Validasi layanan aktif & kuota.
Tentukan nomor tiket (prefix dari D2 + auto-increment per layanan).
Set status awal menunggu, waktu ambil, dan (opsional) identitas singkat.
Hitung estimasi panggilan (berdasarkan D4 & historis D5).
Keluaran
or tiket + estimasi + tautan/QR (opsional) ke User/Pasien.
Daftar tiket per layanan untuk Admin/Pegawai.
D4 berisi tiket baru/terperbarui.
Contoh
en memilih “Poli Umum”; sistem menerbitkan A-037 dan menampilkan estimasi 8 menit.
Ringkasan Arus Data antar Data Store
D1 Users: autentikasi & otorisasi proses 1.0; referensi role untuk 2.0–3.0.
D2 Services: sumber prefix/aturan untuk 4.0; dikelola di 2.0.
D3 Counters: konfigurasi loket untuk 3.0; dikelola di 2.0.
D4 Tickets: siklus hidup tiket (buat–panggil–selesai) untuk 3.0 & 4.0.
D5 Calls: audit panggilan & statistik layanan untuk 3.0 (maupun laporan admin).

2.4.2 Rancagan ERD
Entity Relationship Diagram (ERD) digunakan untuk menggambarkan hubungan antar entitas yang terdapat dalam Sistem Antrian Loket Klinik (SALK). ERD membantu perancang sistem dalam memahami bagaimana data disimpan, diolah, dan saling berhubungan antar tabel di dalam basis data.
Pada sistem SALK, terdapat lima entitas utama yang saling berhubungan, yaitu Users, Services, Counters, Tickets, dan Calls. Kelima entitas ini merepresentasikan struktur data utama dalam proses antrean digital di klinik, mulai dari pengambilan nomor antrean hingga pemanggilan pasien di loket.

Entitas dan Atribut
Users
 Menyimpan data pengguna sistem (admin dan petugas).
 Atribut:
user_id (PK)
username
password
role
nama_lengkap
status_aktif
Services
Berisi data layanan atau poli yang tersedia di klinik.
Atribut:
service_id (PK)
nama_service
prefix
kuota
aktif
Counters
Mewakili loket tempat petugas melayani pasien.
Atribut:
counter_id (PK)
nama_counter
service_id (FK)
petugas_id (FK)
status_counter
Tickets
Menyimpan data tiket antrean pasien.
Atribut:
ticket_id (PK)
nomor_tiket
service_id (FK)
waktu_ambil
status
estimasi_waktu
Calls
Menyimpan riwayat pemanggilan antrean oleh petugas.
Atribut:
call_id (PK)
ticket_id (FK)
counter_id (FK)
petugas_id (FK)
waktu_panggil
catatan

Hubungan Antar Entitas
Hubungan antar entitas pada ERD Sistem SALK dijelaskan sebagai berikut:
Users → Counters (1:N) : Satu petugas dapat bertugas di beberapa loket.
Services → Counters (1:N) : Satu layanan/poli dapat memiliki beberapa loket.
Services → Tickets (1:N) : Satu layanan dapat memiliki banyak antrean pasien.
Counters → Calls (1:N) : Satu loket dapat melakukan banyak pemanggilan antrean.
Tickets → Calls (1:1) : Satu tiket hanya dapat dipanggil satu kali oleh petugas.
Users → Calls (1:N) : Satu petugas dapat memanggil banyak antrean pasien.

Deskripsi Alur ERD
Secara umum, admin membuat data layanan dan menugaskan petugas pada loket tertentu.
Pasien mengambil nomor antrean berdasarkan layanan yang dipilih, kemudian sistem mencatat tiket pada tabel Tickets.
Ketika tiba giliran, petugas memanggil pasien dan sistem mencatat data pemanggilan tersebut dalam tabel Calls.
Setiap aktivitas ini saling terhubung untuk membentuk sistem antrean digital yang terintegrasi dan efisien.


Gambar 2.3 ERD
2.4.3 Rancangan Antarmuka (UI/UX)
Rancangan antarmuka dibuat agar pengguna dapat berinteraksi dengan sistem secara mudah dan intuitif. Pada SALK, terdapat dua jenis antarmuka utama, yaitu antarmuka admin dan petugas.
Halaman Utama Antarmuka Admin
Antarmuka admin pada sistem SALK dirancang agar mudah digunakan dan memudahkan pengelolaan seluruh komponen antrean. Admin memiliki akses penuh terhadap data pengguna, layanan, loket, serta laporan aktivitas sistem.

Fitur utama pada halaman admin meliputi:
Manajemen Pengguna (Users Management) – menambah, mengedit, dan menghapus akun petugas.
Manajemen Layanan (Service Management) – menambah atau menonaktifkan layanan/poli klinik, mengatur prefix tiket, dan menentukan kuota harian.
Manajemen Loket (Counter Management) – mengatur penugasan petugas pada loket tertentu serta status aktif atau nonaktif.
Laporan Aktivitas (Activity Report) – menampilkan statistik antrean harian seperti jumlah tiket, waktu rata-rata pelayanan, dan tingkat keaktifan loket.


Gambar Halaman Utama Antarmuka Admin

Halaman Utama Antarmuka Petugas
Antarmuka petugas digunakan untuk mengelola antrean secara langsung selama jam operasional klinik. Tampilan ini dibuat sederhana agar petugas dapat fokus pada proses pemanggilan pasien.

Fitur utama yang tersedia antara lain:
Daftar Antrean Aktif – menampilkan daftar nomor antrean pasien yang sedang menunggu.
Tombol Panggil / Ulang / Selesai – memanggil pasien berikutnya, mengulang pemanggilan, atau menandai antrean sebagai selesai.
Tampilan Display Real-Time – menampilkan nomor yang sedang dipanggil di layar besar (display) yang terhubung ke sistem.
Riwayat Panggilan – mencatat semua pemanggilan yang telah dilakukan sebagai laporan aktivitas petugas.


Gambar Halaman Utama Antarmuka Petugas





























DAFTAR PUSTAKA
Al-Jami’ah Research Centre. (2024). Al-Jami’ah: Journal of Islamic Studies, 62(2), 145–180. UIN Sunan Kalijaga. https://aljamiah.or.id/ajis


Adeoye, W. A., Erah, P. O., & Macauley, B. O. (2021). Using the queuing model to evaluate and predict optimum outpatient pharmacy dispensing service in Lagos University Teaching Hospital. West African Journal of Pharmacy, 32(1), 61–73. https://doi.org/10.60787/wapcp-32-1-230


Bahadori, M., Mohammadnejhad, S. M., Ravangard, R., & Teymourzadeh, E. (2014). Using queuing theory and simulation model to optimize hospital pharmacy performance. Iranian Red Crescent Medical Journal, 16(3), e16807. https://doi.org/10.5812/ircmj.16807


Acta Medica Indonesiana. (2024). Acta Medica Indonesiana, 56(2), 97–106. Indonesian Society of Internal Medicine. https://actamedindones.org/
Langote, M., Saratkar, S., Kumar, P., Verma, P., Puri, C., Gundewar, S., & Gourshettiwar, P. (2024). Human–computer interaction in healthcare: Comprehensive review. AIMS Bioengineering, 11(3), 343–390. https://doi.org/10.3934/bioeng.2024018


Indonesian Society for Knowledge and Human Development. (2024). International Journal on Advanced Science, Engineering and Information Technology (IJASEIT), 14(2), 505–514. https://ijaseit.insightsociety.org/
Jogiyanto, H. M. (2005). Analisis dan Desain Sistem Informasi: Pendekatan Terstruktur Teori dan Praktek Aplikasi Bisnis. Andi Offset.https://opac.perpusnas.go.id/DetailOpac.aspx?id=436575


Universitas Pendidikan Indonesia. (2024). Indonesian Journal of Science and Technology (IJoST), 9(3), 189–200. https://ejournal.upi.edu/index.php/ijost/


Science and Technology Indonesia Editorial Board. (2024). Science and Technology Indonesia, 9(2), 112–120. https://sciencetechindonesia.com/


Center for the Study of Islam and Society. (2024). Studia Islamika, 31(1), 55–76. http://journal.uinjkt.ac.id/index.php/studia-islamika


Universitas Andalas. (2024). Jurnal Nasional Teknologi dan Sistem Informasi (TEKNOSI), 13(1), 22–34. https://sinta.kemdikbud.go.id/journals/detail?id=50


STIMIK Bina Bangsa Kendari. (2024). Jurnal Sistem Informasi dan Sistem Komputer (JSISKom), 10(1), 15–26. https://sinta.kemdikbud.go.id/journals/profile/10304


Jakarta School of Information and Computer Technology. (2023). Jurnal Ilmiah Komputasi, 12(2), 88–97. https://ejournal.jak-stik.ac.id/index.php/komputasi


Faculty of Computer Science, Universitas Indonesia. (2024). Jurnal Sistem Informasi (Journal of Information System), 20(2), 101–115. https://sinta.kemdikbud.go.id/journals/profile/1085


Universitas Serambi Mekkah. (2023). Jurnal Nasional Komputasi dan Teknologi Informasi (JNKTI), 8(1), 34–45. https://sinta.kemdikbud.go.id/journals/profile/12225


STMIK Lombok. (2021). MISI: Jurnal Manajemen Informatika dan Sistem Informasi, 4(1), 12–22. https://e-journal.stmiklombok.ac.id/index.php/misi/article/view/220






