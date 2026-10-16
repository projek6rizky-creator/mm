
# PRODUCT REQUIREMENTS DOCUMENT (PRD)
# Project: Jadwalin

**Versi:** 1.0.0  
**Status:** Draft  
**Platform:** Website  
**Target:** Pengguna personal  
**Bahasa:** Indonesia  

---

## 1. PROJECT OVERVIEW

Jadwalin adalah website personal untuk mengelola
jadwal pelajaran secara digital.

Pengguna dapat melihat jadwal harian dan mingguan,
menambah atau mengedit jadwal, menerima pengingat
pelajaran, serta mengganti tema website.

### Tujuan
- Memudahkan pengelolaan jadwal pelajaran.
- Menampilkan jadwal secara rapi dan modern.
- Menyimpan jadwal ke database online.
- Memberikan pengingat sebelum pelajaran dimulai.
- Mendukung tema terang dan gelap.

---

## 2. TARGET USERS

Target pengguna adalah siswa yang ingin mengelola
jadwal pelajaran pribadi melalui website.

Kebutuhan pengguna:
- Melihat jadwal hari ini.
- Melihat jadwal satu minggu.
- Menambah, mengubah, dan menghapus jadwal.
- Mengatur pengingat pelajaran.
- Mengganti tema tampilan.
- Mengakses data setelah login kembali.

---

## 3. TECHNOLOGY STACK

Teknologi yang direncanakan:

- Frontend: HTML5, CSS3, JavaScript.
- Database: Supabase PostgreSQL.
- Authentication: Supabase Auth.
- Database Security: Row Level Security (RLS).
- Notifications: Browser Notifications.
- Responsive Design: Mobile, Tablet, Desktop.

Catatan:
Teknologi masih berupa usulan dan belum diimplementasikan.

---

## 4. CORE FEATURES

### 4.1 Authentication
- Login menggunakan akun pribadi.
- Logout dari akun.
- Validasi input dan pesan kesalahan.
- Data setiap pengguna harus terisolasi.

### 4.2 Dashboard
- Menampilkan jadwal hari ini.
- Menampilkan jumlah pelajaran.
- Menampilkan pelajaran berikutnya.
- Menyediakan tombol tambah jadwal.

### 4.3 Weekly Schedule
- Menampilkan jadwal Senin sampai Minggu.
- Menampilkan jam mulai dan selesai.
- Menampilkan nama guru dan ruang kelas.
- Memfilter jadwal berdasarkan hari.

### 4.4 Schedule Management
- Menambah jadwal pelajaran.
- Mengedit jadwal pelajaran.
- Menghapus jadwal dengan konfirmasi.
- Memvalidasi waktu pelajaran.
- Memberikan peringatan jadwal bentrok.

### 4.5 Reminder
- Mengaktifkan atau menonaktifkan pengingat.
- Memilih waktu pengingat.
- Pilihan awal: 5, 10, atau 15 menit.
- Meminta izin notifikasi browser.
- Mendukung Web Push jika diperlukan untuk
  notifikasi ketika website tidak terbuka.

### 4.6 Theme Settings
- Light mode.
- Dark mode.
- Menyimpan tema pilihan pengguna.
- Mempertahankan tema setelah login kembali.

---

## 5. FUNCTIONAL REQUIREMENTS

| ID | Requirement | Priority |
|---|---|---|
| FR-01 | Login dan logout | P0 |
| FR-02 | Dashboard jadwal hari ini | P0 |
| FR-03 | Tampilan jadwal mingguan | P0 |
| FR-04 | Tambah jadwal | P0 |
| FR-05 | Edit jadwal | P0 |
| FR-06 | Hapus jadwal | P0 |
| FR-07 | Penyimpanan database | P0 |
| FR-08 | Deteksi jadwal bentrok | P0 |
| FR-09 | Light dan dark mode | P0 |
| FR-10 | Pengingat pelajaran | P1 |
| FR-11 | Pengaturan profil | P1 |

Priority:
- P0 = Wajib untuk MVP.
- P1 = Fitur tambahan utama.

---

## 6. DATABASE DESIGN

### Table: profiles
- id: UUID, primary key.
- display_name: TEXT.
- created_at: TIMESTAMPTZ.

### Table: subjects
- id: UUID, primary key.
- user_id: UUID, foreign key.
- name: TEXT, required.
- color: TEXT.
- created_at: TIMESTAMPTZ.

### Table: schedules
- id: UUID, primary key.
- user_id: UUID, foreign key.
- subject_id: UUID, foreign key.
- day_of_week: INTEGER, 1-7.
- start_time: TIME, required.
- end_time: TIME, required.
- teacher: TEXT, optional.
- room: TEXT, optional.
- created_at: TIMESTAMPTZ.

### Table: user_settings
- user_id: UUID, primary key.
- theme: TEXT.
- reminder_enabled: BOOLEAN.
- reminder_minutes: INTEGER.
- updated_at: TIMESTAMPTZ.

### Database Rules
- Setiap data dimiliki oleh pengguna tertentu.
- Pengguna hanya dapat mengakses datanya sendiri.
- Terapkan Row Level Security (RLS).
- Waktu selesai harus lebih besar dari waktu mulai.
- Subject harus dimiliki oleh pengguna yang sama.
- Jangan menyimpan kredensial rahasia di frontend.

---

## 7. UI/UX REQUIREMENTS

### Design Direction
- Modern dan minimalis.
- Navigasi sederhana.
- Layout responsif.
- Warna konsisten.
- Tipografi mudah dibaca.
- Mendukung light mode dan dark mode.

### Main Pages
1. Login.
2. Dashboard.
3. Jadwal mingguan.
4. Form tambah/edit jadwal.
5. Pengaturan tema dan pengingat.

### Dashboard Components
- Sidebar atau navigasi responsif.
- Header dan profil pengguna.
- Ringkasan jadwal hari ini.
- Kartu pelajaran berikutnya.
- Daftar pelajaran.
- Tombol tambah jadwal.

---

## 8. NON-FUNCTIONAL REQUIREMENTS

### Security
- Menggunakan autentikasi.
- Mengaktifkan RLS.
- Memvalidasi input.
- Membatasi akses berdasarkan pemilik data.

### Performance
- Menampilkan status loading.
- Menampilkan pesan kesalahan yang jelas.
- Menghindari pengiriman formulir ganda.

### Compatibility
- Mendukung browser modern.
- Mendukung desktop, tablet, dan HP.
- Tampilan menyesuaikan ukuran layar.

### Reliability
- Data tersimpan setelah perubahan berhasil.
- Kegagalan penyimpanan harus ditampilkan.
- Data dimuat kembali dari database.

---

## 9. ACCEPTANCE CRITERIA

Website dinyatakan memenuhi MVP apabila:

1. Pengguna dapat login dan logout.
2. Dashboard menampilkan jadwal yang benar.
3. Pengguna dapat menambah jadwal.
4. Pengguna dapat mengedit jadwal.
5. Pengguna dapat menghapus jadwal.
6. Data tersimpan di database.
7. Jadwal bentrok dapat terdeteksi.
8. Tema dapat diganti dan disimpan.
9. Data tidak dapat diakses pengguna lain.
10. Website berfungsi di HP dan desktop.

Pengingat dinyatakan selesai setelah pengujian
sesuai mekanisme notifikasi yang dipilih.

---

## 10. PROJECT STRUCTURE

jadwalin/
├── index.html
├── pages/
│   ├── login.html
│   ├── dashboard.html
│   ├── jadwal.html
│   └── pengaturan.html
├── css/
│   ├── style.css
│   ├── responsive.css
│   └── themes.css
├── js/
│   ├── app.js
│   ├── auth.js
│   ├── dashboard.js
│   ├── jadwal.js
│   ├── theme.js
│   └── reminder.js
├── services/
│   ├── supabase.js
│   ├── jadwal-service.js
│   └── settings-service.js
├── database/
│   ├── schema.sql
│   └── policies.sql
├── assets/
│   ├── icons/
│   └── images/
├── .env.example
├── README.md
└── PRD.md

---

## 11. DEVELOPMENT ROADMAP

Phase 1: Finalisasi PRD.
Phase 2: Pembuatan wireframe.
Phase 3: Desain UI/UX.
Phase 4: Setup database dan authentication.
Phase 5: Implementasi frontend.
Phase 6: Implementasi reminder.
Phase 7: Testing dan deployment.

---

## 12. OUT OF SCOPE

Fitur yang belum termasuk MVP:
- Multi-user untuk satu kelas.
- Sinkronisasi Google Calendar.
- Aplikasi Android native.
- Integrasi sistem akademik sekolah.
- Ekspor laporan PDF.

---

## 13. PROJECT STATUS

Current Status: Planning / Draft.

Dokumen ini merupakan spesifikasi kebutuhan produk.
Belum ada frontend, database, autentikasi, atau
notifikasi yang diimplementasikan.

Next Step:
Review PRD, finalisasi wireframe, lalu mulai
implementasi berdasarkan persyaratan yang disetujui.
