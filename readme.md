# CharVar - Platform Voting & Leaderboard Karakter Game

## 📌 Deskripsi Proyek
**CharVar** adalah aplikasi web dinamis *end-to-end* yang dibangun untuk memfasilitasi komunitas *gaming* dalam mengurasi daftar karakter favorit dan memberikan suara (voting) untuk menentukan peringkat popularitas karakter. Aplikasi ini menerapkan sistem pembatasan suara maksimal satu kali per minggu untuk setiap pengguna, yang menghasilkan pembaruan **Leaderboard Mingguan** dan **Leaderboard All-Time** secara *real-time*.

Proyek ini dibangun sebagai proyek evaluasi akhir mata kuliah Pemrograman Web menggunakan teknologi *native*: **HTML, CSS, JavaScript, PHP, dan MySQL** tanpa menggunakan *framework* apa pun.

## 🚀 Fitur Utama
Aplikasi ini memiliki tiga level hak akses yang berbeda:

### 1. Fitur Publik (Guest)
*   **Leaderboard:** Melihat daftar peringkat karakter (Top Mingguan & All-Time) berdasarkan jumlah vote tertinggi.
*   **Autentikasi:** Fitur Registrasi (*Sign-up*) dan Login (*Sign-in*) dengan enkripsi kata sandi (*password hashing*).

### 2. Fitur Pengguna Terautentikasi (User)
*   **Katalog Karakter (Ingame Characters):** Menampilkan seluruh karakter dengan fitur *search* (pencarian) dan filter berdasarkan asal *game*.
*   **Sistem Voting Cerdas:** 
    *   Memberikan 1 vote per minggu (divalidasi menggunakan *timestamp* server via PHP).
    *   Dilengkapi **Popup Konfirmasi (Ya/Tidak)** sebelum vote diproses.
    *   Tombol vote otomatis *disabled* jika kuota mingguan sudah habis.
*   **Koleksi Favorit (My Favorites):** Menandai karakter (melalui ikon bintang interaktif menggunakan JavaScript/DOM) dan melihat daftar koleksi pribadi.
*   **Manajemen Sesi:** Fitur aman untuk Logout.

### 3. Fitur Administrator (Admin Panel)
*   **Otorisasi Khusus:** Proteksi halaman berbasis *role* (hanya akun `admin` yang bisa masuk).
*   **CRUD Karakter:**
    *   *Create:* Menambah karakter baru (nama, asal game, URL gambar).
    *   *Read:* Melihat tabel seluruh karakter.
    *   *Update:* Mengedit data karakter yang sudah ada.
    *   *Delete:* Menghapus karakter (otomatis menghapus riwayat vote dan favorit terkait dari database).

## 🗄️ Skema Database
Sistem ini menggunakan 4 tabel utama dalam MySQL:

1.  **Users**
    *   `user_id` (INT, PK, Auto Increment)
    *   `username` (VARCHAR 50, Unique)
    *   `password` (VARCHAR 255)
    *   `role` (ENUM: 'admin', 'user')
    *   `created_at` (TIMESTAMP)
2.  **Characters**
    *   `character_id` (INT, PK, Auto Increment)
    *   `character_name` (VARCHAR 100)
    *   `game_origin` (VARCHAR 100)
    *   `image_url` (VARCHAR 255)
    *   `created_at` (TIMESTAMP)
3.  **Votes**
    *   `vote_id` (INT, PK, Auto Increment)
    *   `user_id` (INT, FK)
    *   `character_id` (INT, FK)
    *   `vote_timestamp` (TIMESTAMP)
4.  **Favorites**
    *   `favorite_id` (INT, PK, Auto Increment)
    *   `user_id` (INT, FK)
    *   `character_id` (INT, FK)
    *   `created_at` (TIMESTAMP)

## 🗺️ Alur Sistem (Sitemap & Storyboard)

**Alur Guest:**
`Landing Page (Leaderboard)` -> `Login / Register` -> Masuk ke Area User/Admin.

**Alur User:**
`Halaman Utama` -> `Ingame Characters (Filter, Vote, Favorite)` -> `My Favorites (Lihat & Hapus)` -> `Logout`.

**Alur Admin:**
`Area Administrator` -> `Dashboard Admin (Tabel Karakter)` -> `Tambah Karakter (Create)` / `Edit Karakter (Update)` / `Delete Karakter` -> `Logout`.

## 🛠️ Cara Menjalankan Proyek (Instalasi Lokal)

1.  **Persiapan Environment:**
    Pastikan Anda sudah menginstal web server lokal seperti **XAMPP**, **Laragon**, atau **MAMP**.
2.  **Clone Repositori:**
    ```bash
    git clone https://github.com/username/charvar-app.git