# Toko Perabot Nusantara

Toko Perabot Nusantara adalah aplikasi web e-commerce yang dirancang untuk menyediakan layanan penjualan berbagai perabotan rumah tangga secara daring. Aplikasi ini dibangun menggunakan Vue.js dan dilengkapi dengan fitur-fitur modern seperti autentikasi pengguna, katalog produk, keranjang belanja, serta checkout dengan berbagai metode pembayaran. Proyek ini dikembangkan dalam rangka tugas akhir mata kuliah Pemrograman Berbasis Komponen (PBK).

## Tujuan Proyek

Proyek ini bertujuan untuk:

1. Mensimulasikan alur transaksi dalam toko online perabotan secara utuh.
2. Menerapkan prinsip-prinsip pemrograman berbasis komponen menggunakan Vue.js.
3. Mengembangkan aplikasi web yang modern, responsif, dan user-friendly.
4. Memberikan pengalaman nyata dalam membangun aplikasi SPA (Single Page Application).

## Fitur Aplikasi

* **Autentikasi Pengguna**:

  * Halaman Login dan Register dengan validasi.
  * Penyimpanan status login menggunakan localStorage.
* **Navigasi Halaman**:

  * Routing menggunakan Vue Router.
  * Navigasi antar halaman: Beranda, Produk, Keranjang, Checkout.
* **Manajemen Produk**:

  * Katalog produk dengan data dinamis.
  * Penambahan produk ke keranjang belanja.
* **Keranjang Belanja**:

  * Tampilan produk yang ditambahkan.
  * Update kuantitas dan total harga.
* **Checkout dan Pembayaran**:

  * Pilihan metode pembayaran: BRI, BCA, BNI, Mandiri, Virtual Account, COD, QRIS.
  * Form isian data kartu untuk metode kartu.
  * Konfirmasi dan notifikasi sukses pembayaran.
* **UI/UX Modern**:

  * Desain responsif dengan Tailwind CSS.
  * Animasi modern dan transisi halus.
  * Navbar dinamis dengan tombol logout dan redirect login.

## Teknologi yang Digunakan

* **Frontend Framework**: Vue 3 (Composition API)
* **Bundler**: Vite
* **Routing**: Vue Router
* **State Management**: Pinia
* **Styling**: Tailwind CSS, CSS Scoped
* **Penyimpanan Data**: LocalStorage (autentikasi & cart)

## Struktur Direktori

```
src/
├── assets/             # Gambar produk dan logo
├── components/         # Komponen UI (Navbar, ProductCard, dll)
├── pages/              # Halaman Login, Register, Beranda, Produk, Keranjang, Checkout
├── router/             # Konfigurasi Vue Router
├── store/              # Pinia Store (cartStore.js)
├── App.vue             # Komponen utama aplikasi
└── main.js             # Inisialisasi Vue app
```


* Aplikasi ini masih menggunakan penyimpanan lokal (localStorage) untuk simulasi login dan data cart.
* Tidak terhubung ke backend atau database.
* Ideal sebagai dasar untuk pengembangan sistem e-commerce yang lebih kompleks.
* Cocok untuk pembelajaran dan tugas akhir berbasis frontend framework.



