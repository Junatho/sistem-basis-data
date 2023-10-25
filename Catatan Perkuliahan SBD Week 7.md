## 📘 SISTEM BASIS DATA

### 🗓️ Week 7: Case Study (1)
### Aktivitas: Merancang Proyek Database (untuk UTS)

### Rancangan Proyek Pengantar Basis Data
#### 📍 1. Deskripsi Sistem
Sistem			: Theater Management System
Deskripsi		: Sistem ini digunakan untuk mengelola operasi sebuah bioskop, di antaranya penjadwalan film, pemesanan kursi, dan penjualan makanan minuman.

#### 📍 2. Tabel Entitas Utama 
Tuliskan nama-nama tabel (entitas) utama yang akan dibuat dalam database beserta deskripsi singkatnya.
Tabel_Film: Tabel ini bertujuan untuk menyimpan data mengenai film yang tersedia dalam bioskop
Tabel_Penayangan: Tabel ini menyimpan informasi jadwal tayang film
Tabel_Pemesanan: Tabel ini untuk mencatat pemesanan tiket oleh pelanggan
Tabel_Pelanggan: Tabel ini untuk menghitung pelanggan yang melakukan pemesanan
Tabel_Kursi: Tabel ini untuk menyimpan informasi kuris di dalam ruang teater
Tabel_MakananMinuman: Tabel ini berisi daftar tentang makanan dan minuman yang tersedia dalam bioskop

#### 📍 3. Atribut Setiap Entitas
Tuliskan nama-nama atribut untuk setiap tabel (entitas) yang telah didefinisikan beserta tipe datanya, batasan integritas (integrity constraint) dan keterangan lainnya (jika ada).
Tabel_Film:
id_film: INT, Primary Key, unik, dan tidak boleh NULL
judul_film: VARCHAR
sutradara: VARCHAR
genre: VARCHAR
tahun_rilis: INT

Tabel_Penayangan:
id_penayangan: INT, Primary Key, unik, dan tidak boleh NULL
id_film: INT, Foreign Key ke Tabel_Film
waktu_mulai: DATETIME
ruang_teater: VARCHAR

Tabel_Pemesanan:
id_pemesanan: INT, Primary Key, unik, dan tidak boleh NULL
id_penayangan: INT, Foreign Key ke Tabel_Penayangan
id_pelanggan: INT, Foreign Key ke Tabel_Pelanggan
jumlah_tiket: INT
total_harga: DECIMAL(10, 2)

Tabel_Pelanggan:
id_pelanggan: INT, Primary Key, unik, dan tidak boleh NULL
nama_pelanggan: VARCHAR
nomor_telepon: VARCHAR
alamat_email: VARCHAR

Tabel_Kursi:
id_kursi: INT, Primary Key, unik, dan tidak boleh NULL
id_penayangan: INT, Foreign Key ke Tabel_Penayangan
nomor_kursi: VARCHAR
tersedia: BOOLEAN

Tabel_MakananMinuman:
id_makanan_minuman: INT, Primary Key, unik, dan tidak boleh NULL
nama_makanan_minuman: VARCHAR
harga: DECIMAL(8, 2)

#### 📍 4. Skema
Tabel_Film(id_film, judul_film, sutradara, genre, tahun_rilis)
Tabel_Penayangan(id_penayangan, id_film, waktu_mulai, ruang_teater)
Tabel_Pemesanan(id_pemesanan, id_penayangan, id_pelanggan, jumlah_tiket, total_harga)
Tabel_Pelanggan(id_pelanggan, nama_pelanggan, nomor_telepon, alamat_email)
Tabel_Kursi(id_kursi, id_penayangan, nomor_kursi, tersedia)
Tabel_MakananMinuman(id_makanan_minuman, nama_item, jenis_item, harga)
