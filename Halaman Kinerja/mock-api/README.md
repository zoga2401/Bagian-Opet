# Mock API Kinerja MAN 5 Jombang

Folder ini menyediakan data JSON contoh agar halaman Kinerja dapat dibuat dan diuji sebelum backend tersedia. Semua dokumen dan angka di sini adalah data tiruan/hanya untuk contoh.

## Struktur

- `categories.json`: urutan kategori, label, ringkasan, jumlah dokumen, dan tahun terbaru.
- `documents/<slug>.json`: daftar dokumen tiap kategori, diurutkan dari tahun/periode terbaru.
- `files/`: tempat manual untuk PDF contoh; lihat `files/README.md`.

Field dokumen mencakup `id` unik, `category`, `title`, `year`, `period_start`/`period_end` (untuk Renstra), `group_label` (pengelompokan), `description`, `file_size` (byte), `page_count`, `allow_download`, `is_sample`, serta `preview`. Pratinjau PDF memakai `preview.type: "pdf"` dan `preview.url`; pratinjau Google Drive memakai `preview.type: "gdrive"` dan `preview.embed_url`.

## Kasus uji

- `zona-integritas` kosong untuk menguji tampilan “Belum ada dokumen”.
- Realisasi Anggaran memiliki subjudul kelompok BOS dan Non-BOS melalui `group_label`.
- Renstra memakai periode 2020–2024 dan 2025–2029 tanpa tahun (`year: null`).
- Salah satu dokumen memakai pratinjau Google Drive.
- DIPA 2025 mengizinkan unduhan; DIPA lainnya tidak.
- Semua entri memakai `is_sample: true`; jumlah dan tahun terbaru kategori mengikuti daftar dokumennya.

## PDF contoh

Taruh sendiri PDF berikut di `mock-api/files/` dengan nama persis: `contoh-pendek.pdf`, `contoh-panjang.pdf`, dan `contoh-besar.pdf`. File PDF tidak disertakan atau dibuat oleh paket ini.

## Endpoint API yang akan digunakan

Bentuk data ini dipertahankan agar dapat dipetakan langsung ke endpoint backend sungguhan nanti:

- `GET /api/kinerja/categories`
- `GET /api/kinerja/documents?category=<slug>`

Jalankan halaman melalui server lokal, misalnya `python -m http.server 8080` dari folder proyek atau gunakan Live Server. `fetch` diblokir oleh browser ketika halaman dibuka langsung memakai `file://`.
