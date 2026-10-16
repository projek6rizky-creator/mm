# Jadwalin

Website personal untuk mengelola jadwal pelajaran: dashboard harian, jadwal mingguan,
tambah/edit/hapus jadwal, deteksi jadwal bentrok, pengingat, dan tema terang/gelap.
Frontend statis (HTML + CSS + JavaScript) dengan backend Supabase (PostgreSQL, Auth, RLS).

## Cara menjalankan

### 1. Buat project Supabase
1. Daftar/login di https://supabase.com lalu buat project baru.
2. Buka **SQL Editor**, jalankan isi `database/schema.sql`, lalu `database/policies.sql`.
3. Buka **Project Settings > API**, salin **Project URL** dan **anon public key**.
4. (Opsional, untuk testing) di **Authentication > Providers > Email**, matikan
   "Confirm email" supaya bisa langsung masuk setelah daftar.

### 2. Isi konfigurasi
Edit `services/supabase.js`, ganti:

```js
export const SUPABASE_URL = "https://YOUR-PROJECT-ID.supabase.co";
export const SUPABASE_ANON_KEY = "YOUR-ANON-PUBLIC-KEY";
```

Pakai **anon key saja**. Jangan pernah memasang `service_role` key di frontend.
Keamanan data dijaga oleh Row Level Security di `database/policies.sql`.

### 3. Jalankan lokal
Karena memakai ES modules, buka lewat server lokal (bukan klik dua kali file HTML):

```bash
cd jadwalin
python3 -m http.server 8000
# buka http://localhost:8000
```

### 4. Deploy
Upload seluruh folder ke hosting statis (Netlify, Vercel, Cloudflare Pages, GitHub Pages).
Tambahkan URL situs kamu di **Supabase > Authentication > URL Configuration**.

## Fitur (sesuai PRD)
- Login, daftar, logout dengan validasi dan pesan error bahasa Indonesia
- Dashboard: jadwal hari ini, jumlah pelajaran, pelajaran berikutnya, tombol tambah
- Jadwal mingguan Senin–Minggu, filter per hari, tampil jam/guru/ruang
- Tambah, edit, hapus (dengan konfirmasi), validasi waktu, peringatan jadwal bentrok
- Pengingat 5/10/15 menit sebelum pelajaran (Browser Notifications)
- Tema terang/gelap yang tersimpan di akun
- Pengaturan profil (nama tampilan)
- Data terisolasi per pengguna lewat RLS

## Catatan
- Pengingat hanya berjalan saat tab Jadwalin terbuka. Web Push (notifikasi saat website
  tertutup) belum dibuat karena butuh service worker dan server push.
- Struktur folder mengikuti `PRD.md`; `js/pengaturan.js` ditambahkan untuk halaman pengaturan.

## Struktur
```
jadwalin/
├── index.html
├── pages/        login, dashboard, jadwal, pengaturan
├── css/          style, responsive, themes
├── js/           app, auth, dashboard, jadwal, pengaturan, theme, reminder
├── services/     supabase, jadwal-service, settings-service
├── database/     schema.sql, policies.sql
└── assets/
```
