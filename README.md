# Matematika Kelas VI — Pendamping Akademik

Paket aplikasi web statis untuk **metode kedua: satu halaman Blogger sebagai portal + GitHub Pages sebagai host aplikasi**. Tidak memakai library, database, atau API berbayar.

## Isi

- `index.html` — tampilan aplikasi.
- `style.css` — tata letak responsif dan warna hijau-emas.
- `app.js` — navigasi satu halaman, soal dan penilaian otomatis, progress lokal, suara opsional, latihan campuran.
- `konten.json` — **66 submateri inti** (4 bab, 11 subbab, 22 materi) dan **12 materi penguatan** (4 modul). Setiap submateri memiliki cerita, penjelasan, contoh diselesaikan bertahap, 1 soal latihan, dan pembahasannya. Total 78 soal mandiri.
- `assets/` — empat ilustrasi foto realistis (.webp) untuk setiap bab. Semua aset dibuat untuk paket ini, tidak menggunakan SVG atau ikon.
- `.nojekyll` — konfigurasi agar GitHub Pages menyajikan berkas statis apa adanya.
- `blogger-embed.html` — kode yang ditempel ke 1 halaman Blogger.
- `build_data.py` — file sumber penyusun konten; **tidak harus diunggah** ke GitHub Pages. Untuk mengedit isi, cukup edit `konten.json` atau script ini.

## A. Publikasi di GitHub Pages

1. Masuk ke GitHub, buat repositori **public** baru, misalnya `matematika-vi-pendamping-akademik`. Bila repositori sudah tersedia, gunakan repositori tersebut; jangan menimpa proyek lain.
2. Unggah berkas `index.html`, `style.css`, `app.js`, `konten.json`, folder `assets/` beserta keempat berkas WebP, dan `.nojekyll` (opsional).
3. Buka **Settings → Pages** di repositori. Pada *Build and deployment*, pilih **Deploy from a branch**, cabang **main**, folder **/(root)**, kemudian simpan.
4. Setelah GitHub menerbitkannya, salin **alamat URL yang benar-benar ditampilkan** di Pages. Biasanya mengikuti format `https://NAMA-PENGGUNA.github.io/NAMA-REPO/`.
5. Buka alamat tersebut di browser untuk menguji Bab 1, tombol berikutnya, latihan, dan penyimpanan tanda selesai.

**Catatan:** situs belum otomatis diterbitkan hanya karena ZIP ini dibuat. Publikasi GitHub dilakukan melalui repositori Anda.

## B. Integrasi satu halaman Blogger

1. Buka `blogger-embed.html` dengan editor teks (Notepad/VS Code).
2. Ganti **semua kemunculan** `TEKS_URL_GITHUB_PAGES` dengan URL dari langkah A.4 **tanpa garis miring terakhir** (misalnya `https://NAMA-PENGGUNA.github.io/matematika-vi-pendamping-akademik`). Sebagai contoh format URL: `https://NAMA-PENGGUNA.github.io/matematika-vi-pendamping-akademik`.
3. Masuk **Blogger → Halaman → Halaman Baru**, berikan judul `Matematika Kelas VI SD/MI | Pendamping Akademik`.
4. Ganti editor menjadi **Tampilan HTML**, tempel seluruh isi `blogger-embed.html`, lalu terbitkan.
5. Uji halaman Blogger, termasuk navigasi pada ponsel. Bila iframe kurang tinggi, ubah `height:900px` di file embed; bila tema menambahkan batas lebar, pengaturan tema mungkin perlu disesuaikan.
6. Menu tautan atas dan tombol `Buka Aplikasi Layar Penuh` tetap tersedia sebagai cadangan jika perangkat membatasi iframe.

## C. Mengedit materi

- Materi disimpan dalam `konten.json` dan dipanggil lewat `fetch()` satu kali saat aplikasi dibuka. Struktur dibangun dari array `lessons`.
- Objek soal memiliki `quiz.question`, `quiz.options` (3 pilihan), `quiz.correct` (indeks 0, 1, 2), `quiz.explanation`.
- Untuk menyunting bab/proyek, lihat `chapters`, `booster`, dan `projects`.
- **Tidak perlu membuat halaman baru** di Blogger untuk memperbaiki isi. Cukup ubah berkas di GitHub Pages, lalu muat ulang aplikasi.

## D. Batasan dan catatan pendidikan

- Paket ini sudah mencakup **seluruh 66 submateri** dengan penjelasan ringkas dan pembahasan contoh; bukan naskah ensiklopedia/buku cetak 360 halaman yang dibahas sebelumnya.
- Buku resmi Matematika Kelas VI menjadi kerangka bab. Rincian submateri dan 4 modul penguatan adalah pengembangan editorial Pendamping Akademik; bukan daftar wajib dari pemerintah.
- Hanya satu soal otomatis per submateri (78 total) serta latihan campuran berisi 10 soal yang dipilih acak dari 78 soal tersebut. Belum ada bank soal ASAJ 1.000 soal, akun guru, atau nilai tersimpan di server.
- `localStorage` dapat dibatasi oleh peramban ketika aplikasi di-embed lintas situs. Data bisa hilang saat cache/data situs dibersihkan dan tidak otomatis mengikuti siswa ke perangkat lain.
- Text-to-speech memakai fitur browser (bila ada) tanpa mikrofon, tidak menjamin ketersediaan suara Bahasa Indonesia pada semua perangkat.
- Pada beberapa tema Blogger, tinggi/ruang iframe perlu diuji dan disesuaikan.

## E. Pengujian lokal

Jalankan dari folder ini:

```bash
python -m http.server 8000
```

Lalu buka `http://localhost:8000/` di browser. Membuka `index.html` dengan skema `file://` tidak dapat mengakses `konten.json` di sebagian browser.

## Sumber teknis

- GitHub Pages: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- Bantuan Blogger: https://support.google.com/blogger/answer/176245?hl=id

## F. Ketentuan visual (revisi)

- Antarmuka aplikasi dan kode Blogger tidak memakai gambar SVG, emoji, atau ikon. Navigasi menggunakan tombol teks.
- Gambar materi berupa **empat ilustrasi foto realistis berbasis AI**, satu untuk masing-masing bab inti. Modul penguatan menggunakan foto dengan konteks paling dekat. Foto bukan dokumentasi siswa/sekolah nyata.
- Seluruh gambar WebP disimpan di folder `assets/`, bukan hotlink. Untuk mengubah foto di masa depan, ganti berkas bersangkutan dengan nama yang sama dan gunakan gambar yang memiliki izin publikasi.
- Isi materi, soal, proyek, dan penyimpanan progres tetap sama seperti paket awal.
