# 📦 Sistem Gudang SPPG (Warehouse Management System)

Sistem Gudang SPPG adalah aplikasi manajemen inventaris tingkat lanjut yang dirancang khusus untuk memantau pergerakan bahan makanan dan operasional pergudangan secara presisi. Berbeda dengan aplikasi kasir (POS) standar, sistem ini menggunakan pendekatan **Ledger-based** (Kartu Stok / Rekening Koran) untuk memastikan akurasi absolut pada setiap mutasi barang.

Aplikasi ini dikembangkan dengan fokus pada performa, keamanan data, serta kompatibilitas penuh dengan lingkungan *Shared Hosting*.

---

## ✨ Fitur Unggulan

*   📊 **Dashboard Analitik Dinamis**: Menampilkan ringkasan metrik secara *real-time* (total item, stok menipis, peringatan kadaluwarsa, dan aktivitas mutasi harian) dengan visualisasi grafik interaktif.
*   📖 **Single Source of Truth (Kartu Stok)**: Saldo barang tidak disimpan secara statis, melainkan selalu dikalkulasi dari riwayat `qty_in` dan `qty_out` layaknya buku rekening bank, memastikan integritas data 100%.
*   🛡️ **Proteksi Stok Minus (Validation)**: Sistem secara otomatis memblokir pengeluaran barang jika *kuantitas* yang diminta melebihi persediaan fisik (saldo) saat ini.
*   📋 **Multi-Item Daily Inspections**: Mendukung fitur pemeriksaan harian (*stock opname*) dengan arsitektur *1 Header - Many Items*, mencatat kecocokan kuantitas dan kondisi fisik (Baik/Rusak).
*   🖨️ **Laporan Komprehensif (PDF & Excel)**: Menghasilkan 7 jenis laporan profesional, termasuk Laporan Stok Masuk/Keluar, Saldo Saat Ini, Kartu Stok, Opname, Barang Kadaluwarsa, dan Barang Butuh Restock.
*   ⏰ **Sistem Manajemen Expired Date**: Memonitor dan memberikan notifikasi otomatis untuk barang yang akan kadaluwarsa dalam 30 hari ke depan.

---

## 🛠️ Teknologi yang Digunakan

*   **Backend Framework:** Laravel 12 (PHP 8.2)
*   **Frontend UI:** Tailwind CSS & Alpine.js (Dioptimalkan untuk *Shared Hosting*, tanpa dependensi Node.js di sisi server).
*   **Database:** MySQL (Relasional ketat dengan *Cascading & Restrict*).
*   **Export/Reporting:** `barryvdh/laravel-dompdf` (PDF) & `maatwebsite/excel` (Excel).
*   **Design System:** Modern Neumorphism & Material Design 3 dengan palet warna eksklusif **Teal (`#006666`)** dan **Navy Blue (`#091426`)**.

---

## 📂 Struktur Database Inti

Sistem ini memiliki relasi database yang kokoh:
1.  `categories`, `units`, `suppliers`, `storage_locations` -> Master Data.
2.  `items` -> Data barang dengan perlindungan `minimum_stock`.
3.  `stock_entries` & `stock_entry_items` -> Transaksi barang masuk beserta *expired date*.
4.  `stock_exits` & `stock_exit_items` -> Transaksi barang keluar.
5.  `inspections` & `inspection_items` -> Pemeriksaan opname fisik.
6.  `stock_cards` -> Buku besar (*Ledger*) pencatat mutasi riil stok absolut.

---

## 🚀 Panduan Instalasi (Development)

Untuk menjalankan proyek ini secara lokal, ikuti langkah-langkah berikut:

```bash
# 1. Install dependensi PHP
composer install

# 2. Persiapkan environment
cp .env.example .env
php artisan key:generate

# 3. Konfigurasi database di file .env Anda
# DB_DATABASE=sistem_gudang_db dsb...

# 4. Jalankan migrasi dan seeder utama (Master Data & Admin)
php artisan migrate:fresh --seed

# 5. Link Storage untuk gambar/dokumen (Opsional)
php artisan storage:link

# 6. Jalankan server lokal
php artisan serve
```

**Kredensial Default:**
*   **Email:** `admin@sppg.local`
*   **Password:** `password`

*(Catatan: Segera ubah password admin default ini setelah aplikasi di-deploy ke production).*

---

## 📡 Deployment ke Hosting (Production)

Sistem ini sangat mudah di-deploy ke CPanel / Shared Hosting karena seluruh aset (CSS/JS) sudah dikompilasi.
1. Ubah `.env` menjadi:
   ```env
   APP_ENV=production
   APP_DEBUG=false
   ```
2. Jalankan perintah optimasi:
   ```bash
   php artisan optimize:clear
   php artisan optimize
   ```
3. Upload file ke hosting Anda.

---

## 👨‍💻 Tentang Pengembang
Dikembangkan sebagai solusi komprehensif untuk menjawab tantangan pengelolaan gudang modern yang membutuhkan tingkat akurasi pencatatan yang tinggi.
