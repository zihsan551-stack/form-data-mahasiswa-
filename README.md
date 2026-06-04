## Deskripsi Aplikasi

STITEK AKADEMIK: Sistem Pengolahan Berkas Mahasiswa adalah sebuah aplikasi berbasis web modern yang dirancang untuk mengelola data dan administrasi mahasiswa secara mandiri, efisien, dan dinamis. Aplikasi ini mengusung pendekatan *Single-Page Application* (SPA) sederhana di mana seluruh operasi manajemen data, validasi, kontrol tampilan, hingga perpindahan tema dilakukan sepenuhnya di sisi klien (*client-side*) tanpa memerlukan muat ulang halaman (*page refresh*).

Aplikasi ini mengintegrasikan antarmuka dua panel (*split-screen layout*) yang memisahkan antara borang data (Form Input) di sisi kiri dan dasbor pemantauan data secara langsung (Live Monitor & Table) di sisi kanan. Seluruh informasi yang diolah disimpan secara persisten di dalam penyimpanan lokal peramban (*browser local storage*), menjadikannya solusi aplikasi manajemen lokal yang tangguh dan siap pakai.

---

## Alur Kerja Sistem (System Workflow)

Sistem pada berkas `"UTS Pemrograman web.html"` bekerja melalui siklus interaksi data sebagai berikut:

1. **Penyimpanan Data Berkelanjutan (Persistence):** Setiap kali halaman dibuka, sistem otomatis memuat data lama dari `localStorage`. Jika data kosong, sistem akan menginisialisasi ruang penyimpanan baru berbentuk larik (*array*) kosong.
2. **Validasi & Interupsi Duplikasi:** Saat pengguna mengirimkan data melalui form, sistem menjalankan fungsi pengecekan otomatis. Sistem akan menolak penyimpanan dan menampilkan pesan peringatan jika ada kolom wajib yang kosong, atau jika ditemukan kesamaan NIM (*Duplicate NIM Checking*) pada mode pembuatan data baru.
4. **Penyaringan Konten Dinamis (Reactive Filtering):** Ketika pengguna mengetik di kolom pencarian atau mengubah opsi pada dropdown jenis kelamin, sistem secara reaktif memotong dan menyaring data utama. Data yang muncul pada tabel langsung berubah sesuai kata kunci secara *real-time*.
5. **Manajemen Pembaruan Aman (Safe Update State):** Saat tombol "Ubah" pada baris tabel diklik, sistem beralih ke mode penyuntingan. Nilai ID data lama dikunci ke dalam input tersembunyi (`editId`) dan kolom NIM dimatikan fungsinya (*disabled*), guna menjamin tidak ada perubahan NIM tidak sengaja yang dapat merusak struktur identitas mahasiswa.
6. **Personalisasi Pengguna (Adaptive Theme):** Pengguna dapat bebas beralih dari mode terang ke mode gelap kapan saja melalui tombol saklar di pojok kanan atas. Preferensi visual ini langsung disimpan oleh sistem agar pengalaman visual pengguna tetap konsisten saat mereka kembali membuka aplikasi di lain waktu.

## Analisis Komponen Antarmuka (UI Component Breakdown)

<img width="1902" height="901" alt="Screenshot 2026-06-04 225153" src="https://github.com/user-attachments/assets/9113b7da-91db-4e2b-bbc8-06b4974a3bdc" />

Berdasarkan gambar yang sesuai dengan yang diatas, tata letak aplikasi dibagi menjadi dua area fungsional utama dengan struktur komponen sebagai berikut:

### 1. Panel Formulir Kiri (Sidebar Input Panel)

<img width="496" height="690" alt="image" src="https://github.com/user-attachments/assets/91d42287-df7a-4745-ab75-2ec8995fcac7" />

Berfungsi sebagai pusat kendali untuk memasukkan dan memanipulasi data mahasiswa.
* **Header Instansi:** Menampilkan nama sistem **"STITEK AKADEMIK"** dengan sub-judul *"Sistem Pengolahan Berkas Mahasiswa"*.
* **Judul Dinamis:** Teks *"Tambah Mahasiswa"* yang akan berubah menjadi *"Ubah Data Mahasiswa"* secara otomatis saat mode edit aktif.
* **Input Fields:** Elemen masukan berdesain minimalis dengan *placeholder* penunjuk yang terdiri dari:
  * Batas kolom isi **NIM Mahasiswa**.
  * Batas kolom isi **Nama Lengkap**.
  * Batas kolom isi **Alamat Domisili**.
  * Menu pilihan (*Dropdown*) **Jenis Kelamin**.
  * Batas kolom rahasia **Kata Sandi Akun**.
* **Tombol Aksi Utama:** Tombol **"Simpan Data"** berwarna biru cerah (`--primary`) yang meluas penuh (*full-width*) di bagian bawah formulir.

### 2. Panel Utama Kanan (Dasbor Pemantauan & Tampilan Data)

<img width="1405" height="898" alt="image" src="https://github.com/user-attachments/assets/415e6d50-a32a-4783-b867-3635bf3b0e80" />

Berfungsi sebagai pusat visualisasi data, statistik ringkas, serta pengelolaan penyaringan data.
* **Bilah Atas (Top Toolbar):** Berisi judul halaman *"Dasbor Pemantauan"* dan tombol saklar tema berbentuk lingkaran di sudut kanan atas yang menampilkan ikon matahari (☀️), menandakan sistem sedang berada dalam **Mode Terang**.
* **Kartu Metrik Statistik (Metrics Grid):** Tiga kartu ringkasan dengan garis tepi kiri berwarna kontras untuk mempermudah pemindaian informasi:
  * **TOTAL MAHASISWA:** Indikator akumulasi seluruh data (saat ini bernilai `0`)
  * **LAKI-LAKI (L):** Indikator jumlah mahasiswa laki-laki (saat ini bernilai `0`)
  * **PEREMPUAN (P):** Indikator jumlah mahasiswa perempuan (saat ini bernilai `0`).
* **Pusat Kontrol & Filter (Filter Hub):** Barisan kontrol horizontal yang terdiri dari kolom pencarian berbasis teks (*Cari Berdasarkan NIM / Nama...*), *dropdown* filter gender (*Semua Jenis Kelamin*), dan *dropdown* pengurutan (*Urutan Default*).
* **Tabel Data Dinamis:** Tabel responsif untuk menampilkan berkas mahasiswa. Pada kondisi awal (data kosong), tabel menampilkan keadaan *Empty State* berupa teks abu-abu di tengah bertuliskan: **"Tidak ada kecocokan data mahasiswa."**.
* **Kontrol Halaman (Pagination):** Tombol angka indeks halaman (aktif pada halaman `1`) yang terletak tepat di bawah tabel untuk navigasi antar-halaman data.

* ## Fitur Utama (Key Features)

Aplikasi ini dilengkapi dengan berbagai fitur manajemen data dinamis bawaan:

<img width="1903" height="897" alt="image" src="https://github.com/user-attachments/assets/d6013925-775c-40b4-a497-6ed1bf5ee5b8" />


* **Manajemen CRUD Lengkap (Create, Read, Update, Delete):** 
  * Menambah data mahasiswa baru dengan validasi instan.
  * Mengubah data (*Update*) dengan fitur penguncian NIM otomatis untuk mencegah duplikasi identitas berkas.
  * Menghapus data permanen dengan konfirmasi keamanan.
* **Dasbor Pemantauan Real-Time (Metrics Dashboard):** 
  * Menampilkan jumlah total mahasiswa terdaftar serta statistik otomatis pembagian jumlah gender secara real-time.
* **Pencarian & Filter Hub:**
  * Pencarian data adaptif berdasarkan kecocokan NIM maupun Nama Lengkap secara langsung saat mengetik (*on-input*).
  * Penyaringan (*filtering*) data berdasarkan kategori Jenis Kelamin.
* **Pengurutan Berkas (Sorting):** 
  * Mengurutkan daftar nama mahasiswa secara alfabetis dari A - Z maupun sebaliknya (Z - A).
* **Paginasi Data (Pagination):** 
  * Pembatasan tampilan data (3 baris per halaman) untuk menjaga kerapian tata letak antarmuka saat data berjumlah banyak.
* **Manajemen Tema Fleksibel:** 
  * Fitur *switch* tema Terang/Gelap yang responsif dilengkapi dengan perubahan ikon indikator (☀️/🌙) dan penyimpanan preferensi menggunakan `localStorage`.

---

## Penjabaran Teknis & Arsitektur Kode

Aplikasi ini dibangun dalam satu berkas tunggal (*single-file architecture*) **"UTS Pemrograman web.html"**.

### 1. Tanpa Framework (Pure Vanilla Architecture)
Proyek ini **tidak menggunakan framework JavaScript atau CSS apa pun** (seperti Bootstrap, Tailwind CSS, React, Vue, atau Angular).
* **Pewarnaan & Desain (CSS):** Menggunakan **CSS3 Native** murni. Fitur manajemen tema terang/gelap diatur secara mandiri menggunakan variabel bawaan CSS (*CSS Custom Properties*) seperti `--primary` dan `--bg-main`, serta pengaturan tata letak menggunakan **CSS Grid** dan **Flexbox** standar.
* **Logika & Manipulasi Data (JavaScript):** Menggunakan **Vanilla JavaScript (ES6+)** murni. Seluruh fungsi interaktif mulai dari penanganan form, penyaringan data, pengurutan, pemotongan halaman, hingga penyimpanan data, dilakukan secara langsung memanfaatkan API bawaan peramban seperti DOM Manipulation dan `localStorage`.

### 2. Skema Objek Mahasiswa & Penyimpanan
Data mahasiswa dikelola dalam bentuk *Array of Objects* dan disinkronisasikan secara persisten ke `localStorage` dengan nama kunci `"mahasiswa"`.

### 3. Bedah Fungsi Global & Arsitektur Fungsi (Deep Dive Functions)

Sistem interaktif pada aplikasi ini digerakkan oleh beberapa fungsi JavaScript utama yang saling terintegrasi untuk menjaga sinkronisasi antara data (*state*) dan tampilan (*view*):

#### A. Fungsi `render()` (The Central View Engine)
Fungsi ini adalah jantung dari aplikasi yang bertugas memperbarui seluruh aspek visual setiap kali terjadi perubahan data atau interaksi pengguna.
* **Reaktivitas Total:** Di dalam fungsi ini, metrik statistik dihitung ulang menggunakan manipulasi array `.filter()`. 
* **Pipa Pemrosesan Bertingkat:** Fungsi ini menggabungkan tiga operasi array sekaligus: menyaring data berdasarkan teks pencarian dan jenis kelamin, mengurutkan hasil penyaringan berdasarkan nama, lalu memotong (*slicing*) hasilnya untuk kebutuhan paginasi halaman aktif.
* **Penanganan Data Kosong (*Empty State*):** Jika hasil pencarian atau penyaringan menghasilkan array kosong (`rows.length === 0`), fungsi ini secara dinamis menyuntikkan baris khusus (`<tr>`) ke dalam `<tbody>` yang menampilkan pesan *"Tidak ada kecocokan data mahasiswa."* agar antarmuka tidak terlihat rusak atau terpotong.

#### B. Fungsi `edit(id)` & `resetFormState()` (State Swapping)
Dua fungsi ini bertanggung jawab penuh dalam mengelola transisi antarmuka formulir antara mode penambahan data baru dan mode koreksi data.
* **Fungsi `edit(id)`:** Berfungsi mencari objek mahasiswa berdasarkan ID unik menggunakan `.find()`. Setelah data ditemukan, fungsi ini memindahkan nilai objek ke masing-masing elemen input formulir, mengunci kolom NIM (`disabled = true`), dan mengubah teks tombol serta judul formulir menjadi *"Terapkan Koreksi"* untuk memberikan petunjuk visual yang jelas kepada pengguna.
* **Fungsi `resetFormState()`:** Berfungsi mengembalikan formulir ke kondisi semula menggunakan metode bawaan `.reset()`. Selain itu, fungsi ini membuka kembali kuncian pada kolom NIM, menyembunyikan tombol *"Batalkan Perubahan"*, serta membersihkan seluruh sisa pesan kesalahan/galat (`error-message`) yang sempat muncul dari proses validasi sebelumnya.

#### C. Fungsi `hapus(id)` (Data Destructuring with Confirmation)
* Fungsi ini memicu jendela dialog bawaan peramban menggunakan `confirm()` untuk memastikan tindakan penghapusan berkas benar-benar disengaja oleh pengguna.
* Jika disetujui, data dihapus dari array utama menggunakan metode mutasi imutabel `.filter(d => d.id !== id)`. Selanjutnya, data terbaru langsung disimpan kembali ke `localStorage` dan fungsi `render()` dipanggil ulang untuk memperbarui tabel secara instan.
* **Proteksi Halaman Paginasi:** Di dalam fungsi `render()`, terdapat baris proteksi `if (page > totalPage) page = totalPage;`.
 Proteksi ini mencegah terjadinya halaman kosong (*blank page*) jika pengguna menghapus seluruh data yang berada di halaman terakhir.

#### D. Penanganan Event Pendengar (Event Listeners)
* **`search.oninput`:** Menggunakan interaksi reaktif di mana setiap kali pengguna mengetik satu karakter di kolom pencarian, sistem otomatis mengembalikan halaman aktif ke angka `1` (`page = 1`) dan mengeksekusi `render()`. Ini memberikan pengalaman pencarian instan tanpa perlu menekan tombol "Cari".
* **`form.onsubmit`:** Berfungsi menginterupsi perilaku bawaan browser (`e.preventDefault()`) agar halaman tidak memuat ulang.
Fungsi ini bertindak sebagai gerbang validasi utama sebelum data masuk ke memori penyimpanan.
