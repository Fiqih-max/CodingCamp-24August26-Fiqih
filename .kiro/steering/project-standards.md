# Project Standards — Life Dashboard

Konteks ini selalu disertakan saat bekerja di project ini. Patuhi aturan di bawah untuk semua perubahan.

## Ringkasan project

Life Dashboard adalah aplikasi web front-end personal yang menggabungkan to-do list, focus timer (pomodoro), jam/kalender, dan quick links dalam satu halaman. Tidak ada backend; semua data persisten disimpan di browser lewat Local Storage.

## Tech stack

- **HTML** — satu file `index.html`, semantic markup, `lang="en"`, viewport meta aktif.
- **CSS** — murni CSS (bukan Sass/Less/Tailwind). Menggunakan CSS custom properties (variables) untuk theming. Font: Bricolage Grotesque via Google Fonts.
- **JavaScript** — Vanilla JavaScript (ES6+), tanpa framework (tanpa React/Vue/jQuery), tanpa build step, tanpa bundler, tanpa NPM dependencies. Tidak ada TypeScript.
- **Persistence** — `localStorage` dengan helper `load(key, fallback)` dan `save(key, value)` yang membungkus `JSON.parse`/`JSON.stringify`. Selalu bungkus akses localStorage dalam try/catch.
- **Tidak ada backend/API** — semua state ada di sisi klien. Jangan menambahkan fetch/XHR ke server atau dependency eksternal.

## Struktur folder (WAJIB dipatuhi)

```
/
├── index.html          # satu-satunya file HTML, entry point
├── css/
│   └── style.css       # SATU file CSS. Dilarang menambah file CSS lain.
└── js/
    └── script.js       # SATU file JS. Dilarang menambah file JS lain.
```

Aturan ketat:
- **Hanya boleh ada 1 file CSS**, yaitu `css/style.css`. Jangan buat file CSS kedua, jangan pecah menjadi partial, jangan gunakan CSS-in-JS atau preprocessor. Semua styling baru ditambahkan ke `style.css` yang sudah ada.
- **Hanya boleh ada 1 file JS**, yaitu `js/script.js`. Jangan buat file JS kedua, jangan pecah menjadi modul terpisah, jangan gunakan ES module import/export antar-file. Semua logic baru ditambahkan ke `script.js` yang sudah ada.
- **`index.html`** adalah satu-satunya HTML file. Referensi CSS dan JS di dalamnya harus tetap menunjuk ke `css/style.css` dan `js/script.js`.
- Struktur ini sengaja dijaga minimal untuk project ini. Hindari membuat subfolder baru.

## Konvensi kode

CSS:
- Theming lewat CSS variables di `:root` dan override pada `[data-theme="dark"]`. Tambah variabel baru di kedua blok itu agar tema terang/gelap konsisten.
- Kelas BEM-ish ringan, nama sederhana (`.card`, `.btn`, `.btn.ghost`, `.link-chip`). Ikuti pola penamaan yang sudah ada.
- Responsive: breakpoint utama `@media (max-width: 760px)`. Hormati `@media (prefers-reduced-motion: reduce)`.
- Gunakan `var(--nama)` untuk warna, jangan hardcode nilai hex di luar `:root`.

JavaScript:
- Helper `$` = `document.getElementById(id)`. Gunakan ini untuk mengambil elemen, bukan `querySelector` kecuali perlu selector kompleks.
- Struktur file dibagi dengan komentar pembatas `// ---------- Bagian ----------`. Tambahkan fitur baru sebagai bagian baru dengan pola komentar yang sama.
- Event-driven: pasang listener langsung pada elemen, lakukan render ulang (`renderTasks`/`renderLinks`) setelah mutasi data lalu simpan ke localStorage.
- Semua user input string harus di-trim (`value.trim()`) dan divalidasi sebelum dipakai/disimpan.
- Tidak boleh ada `alert`/`prompt` kecuali sudah menjadi pola yang ada (timer selesai pakai `alert`).
- ID record pakai `Date.now()` seperti pola yang sudah ada.

## Hal yang tidak boleh dilakukan

- Jangan menambah framework, library, atau dependency NPM.
- Jangan menambah file CSS atau JS kedua.
- Jangan memecah file yang sudah ada menjadi beberapa file.
- Jangan mengubah referensi `<link rel="stylesheet" href="css/style.css">` dan `<script src="js/script.js">` di `index.html`.
- Jangan menambahkan backend, API call, atau service worker.
