# SIRI-DLHK — Sistem Informasi Retribusi Sampah Rumah Tangga

Aplikasi web (prototipe/simulasi) untuk pengelolaan **retribusi sampah rumah tangga** di lingkungan Dinas Lingkungan Hidup & Kebersihan (DLHK) Kota Jayapura. Aplikasi menyediakan dasbor, manajemen data pengguna & klien, tagihan, pembayaran QRIS, laporan, serta pemantauan aktivitas pengguna.

> Catatan: Ini adalah prototipe front-end murni (tanpa backend). Seluruh data bersifat contoh/simulasi dan disimpan di memori (state Alpine.js) serta `localStorage` untuk sesi login.

## Teknologi

- **HTML5** statis (tanpa proses build).
- **Tailwind CSS** via CDN untuk styling.
- **Alpine.js v3** via CDN untuk interaktivitas (state, modal, filter, tab).
- **Font Awesome 6** untuk ikon.

## Struktur Berkas

```
211-siri-dlhk/
├── index.html      # Aplikasi utama (dasbor & seluruh halaman setelah login)
├── login.html      # Halaman simulasi login untuk semua peran
├── img/
│   ├── logo-kota-jayapura.png   # Logo & favicon
│   └── logo-nokensoft.jpg       # Logo footer
└── README.md
```

## Peran Pengguna (Roles)

Sistem memiliki empat peran dengan hak akses dan metode login berbeda:

- **Admin Master** — akses penuh: kelola Operator DLHK, Operator Kelurahan, Klien, Laporan, dan Aktivitas.
- **Operator DLHK** — kelola Operator Kelurahan, Klien, Laporan, dan Aktivitas.
- **Operator Desa / Kelurahan** — kelola data Klien di wilayahnya, Laporan, dan Aktivitas.
- **Klien** — melihat Tagihan pribadi, melakukan pembayaran (QRIS), Laporan, dan Aktivitas.

### Metode Login (simulasi)

- **Klien**: login menggunakan **NPWRD** + **kode verifikasi acak**.
- **Operator Desa, Operator DLHK, Admin Master**: login menggunakan **username**, **password**, dan **kode verifikasi acak**.

Pada halaman `login.html`, kredensial apa pun diterima selama **kode verifikasi** diisi dengan benar (karena ini simulasi). Setelah berhasil, peran disimpan ke `localStorage` dan pengguna diarahkan ke `index.html?role=<peran>`.

## Fitur Utama

### Autentikasi & Sesi
- Halaman login dengan pemilih peran dan kode verifikasi acak (dapat di-refresh).
- Toggle lihat/sembunyikan password untuk operator/admin.
- Logout via dropdown pengguna di kanan atas (membersihkan sesi `localStorage`).

### Navigasi Berbasis Peran
- Menu sidebar otomatis menyesuaikan peran yang sedang aktif.
- Dropdown informasi pengguna (nama & peran) di header dengan tombol keluar.

### Dasbor
- Kartu statistik ringkas (menyesuaikan peran).
- Grafik realisasi retribusi bulanan (SVG) dan ringkasan status tagihan.
- Tabel aktivitas pembayaran terbaru.

### Manajemen Data
- **Operator DLHK**, **Operator Kelurahan**, dan **Klien**: pencarian, filter, tambah, ubah, dan hapus data (modal).
- Kolom **Distrik** ditampilkan pada tabel Klien dan Operator Kelurahan.
- **Tempat Sampah** pada setiap tabel data untuk melihat & memulihkan data terhapus (simulasi).
- **Detail Klien** dipisah menjadi dua tab: **Detail Klien** (profil) dan **Transaksi Retribusi** (riwayat pembayaran klien).

### Tagihan & Pembayaran (Klien)
- Daftar tagihan dengan status (Lunas / Belum Bayar / Menunggak).
- Pembayaran via **QRIS** (modal QR simulasi).

### Laporan
- Pencarian dan filter berdasarkan **Bulan**, **Distrik**, **Kelurahan**, dan **Status**.
- Ringkasan total terkumpul, belum lunas, dan menunggak.
- **Ekspor Excel** langsung dari tabel yang sedang tampil (mengikuti filter aktif).

### Aktivitas Pengguna
- Riwayat aktivitas yang disesuaikan dengan peran (login, tambah/ubah/hapus data, pembayaran, dll).
- Panel **Pengguna Sedang Aktif** menampilkan sesi pengguna yang sedang login/online beserta status dan waktu aktif terakhir.

## Cara Menjalankan

Karena murni statis, cukup buka berkas di browser:

1. Buka `login.html` di browser (klik dua kali atau seret ke jendela browser).
2. Pilih peran, isi kredensial, dan masukkan kode verifikasi yang tampil.
3. Setelah masuk, Anda diarahkan ke `index.html`.

Opsional, jalankan via server lokal agar path aset & `localStorage` lebih konsisten:

```bash
# Python 3
python -m http.server 8080
# lalu buka http://localhost:8080/login.html
```

> Tips: Jika perubahan tidak tampil, lakukan **hard refresh** (Ctrl+F5) atau aktifkan *Disable cache* di DevTools untuk melewati cache browser.

## Keterbatasan

- Tidak ada backend/basis data — seluruh data adalah contoh dan tidak persisten (kecuali peran/sesi di `localStorage`).
- Operasi tambah/ubah/hapus, unduh, dan pembayaran bersifat simulasi UI.
- Memerlukan koneksi internet untuk memuat CDN (Tailwind, Alpine.js, Font Awesome).

## Kredit

Dikembangkan untuk Dinas Lingkungan Hidup & Kebersihan Kota Jayapura.
Powered by [Nokensoft.com](https://nokensoft.com).
