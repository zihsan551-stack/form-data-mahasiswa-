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

Contoh Antarmuka

