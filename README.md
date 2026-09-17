# Template Web Frontend - Singkong Language Integration

Project ini merupakan *frontend web template* berbasis **Bootstrap 5** dan **AdminLTE 4** yang dirancang khusus untuk memenuhi kualifikasi *technical test* serta siap diintegrasikan dengan bahasa/interpreter **Singkong**.

Terdapat **2 versi penyajian** dalam repository ini untuk memudahkan pengujian di berbagai lingkungan (*offline/pure-static* maupun *server-side/interpreter*).

---

## 📁 Struktur Folder

template-web/
├── 01-pure-static/             # [UTAMA] Versi Pure Static (Zero-CDN & CORS-Free)
│   ├── assets/
│   │   ├── css/                # Bootstrap 5, AdminLTE 4, Custom Style
│   │   ├── js/                 # jQuery 3.7.1, Bootstrap Bundle, ECharts
│   │   └── img/                # Asset Gambar & Logo
│   ├── index.html              # Dashboard Utama
│   ├── feature1.html           # Halaman Contoh Feature 1
│   └── contact.html            # Halaman Contoh Contact
│
├── 02-singkong-version/        # [INTEGRASI] Versi Modular Interpreter Singkong
│   ├── assets/                 # Copy dari aset statis
│   ├── views/
│   │   ├── partials/
│   │   │   ├── header.singkong # Layout Navbar Desktop & Dropdown User
│   │   │   └── sidebar.singkong# Layout Sidebar Mobile Overlay
│   │   └── pages/
│   │       ├── dashboard.singkong
│   │       └── feature1.singkong
│   └── index.singkong          # Entry point utama Singkong
│
└── README.md

## 🚀 Fitur & Kepatuhan Spesifikasi UI

| No | Spesifikasi Requirement | Detail Implementasi | Status |
| --- | --- | --- | --- |
| 1 | **Brand Logo** | Tampil di pojok kiri atas (Top-Left Navbar). | ✅ |
| 2 | **Top Navbar Menu** | Menu utama tampil di bagian atas untuk layar Desktop (`d-none d-md-flex`). | ✅ |
| 3 | **Mobile Sidebar Overlay** | Hanya tampil di layar mobile (`d-md-none`) menggunakan Bootstrap *Offcanvas* (`offcanvas-start`). Menutup area screen tanpa mendorong konten. | ✅ |
| 4 | **Mobile Hamburger Position** | Tombol hamburger diletakkan **sebelum** Brand Logo pada mode mobile. | ✅ |
| 5 | **Active State Indicator** | Penanda class CSS `.active` diimplementasikan secara jelas di Navbar Desktop dan Sidebar Mobile. | ✅ |
| 6 | **Dropdown User Z-Index** | Dropdown profile user di kanan atas berada di layer teratas (`z-index: 1060`), lebih tinggi dari overlay sidebar mobile (`z-index: 1045`). | ✅ |
| 7 | **Zero CDN / Pure Offline** | Seluruh aset (CSS, JS, Fonts, Images) disimpan secara lokal. Bebas isu CORS saat dibuka via protokol `file://`. | ✅ |

---

## 🛠️ Tech Stack

* **CSS Framework:** Bootstrap 5.3.x & AdminLTE 4
* **Icons:** Bootstrap Icons (Local Fonts)
* **JavaScript Library:** jQuery v3.7.1 (dengan alias `q`)
* **Data Visualization:** ECharts (Local script)
* **Backend / Interpreter:** Singkong Language (`.singkong`)

---

## 💻 Cara Menjalankan

### 1. Versi Pure Static (`01-pure-static/`)

Diperuntukkan untuk pengujian cepat tanpa memerlukan server lokal / interpreter:

1. Masuk ke folder `01-pure-static/`.
2. Klik ganda (*double-click*) file `index.html` untuk memuat halaman utama di browser apa saja.
3. Seluruh fitur (Dashboard, ECharts, Mobile Sidebar, Dropdown) dijamin berjalan mulus 100% tanpa kendala CORS.

### 2. Versi Singkong Interpreter (`02-singkong-version/`)

Diperuntukkan untuk integrasi *server-side* dengan interpreter Singkong:

1. Pastikan *environment* / runtime Singkong sudah terpasang.
2. Jalankan entry point utama `index.singkong`.
3. Template menggunakan arsitektur modular (`@include`) untuk memisahkan bagian `header.singkong`, `sidebar.singkong`, dan konten halaman.

---

## 🎨 Penyesuaian CSS Penting (`assets/css/style.css`)

Untuk menjaga hirarki *layering* (z-index) antara header, dropdown user, dan mobile offcanvas sidebar agar tidak saling memotong, override CSS berikut diterapkan:

```css
/* Header sticky dengan Z-Index tinggi */
.app-header {
  position: sticky;
  top: 0;
  z-index: 1050 !important;
  height: 56px;
}

/* Dropdown User selalu di layer paling atas */
.app-header .dropdown-menu {
  z-index: 1060 !important;
}

/* Offcanvas Sidebar meluncur tepat di bawah Header */
#mobileSidebar.offcanvas-start {
  top: 56px !important;
  height: calc(100vh - 56px) !important;
}

```

