# Panduan Kerja 5 Orang — Gacha Quest

Starter kit ini hanya berisi panduan, bukan kode atau jawaban.
Rencana induk: `rencana-pembagian-tugas-5-orang.md`.

Baca berurutan:

1. `panduan-0-git-dan-kompilasi.md` — wajib untuk semua orang.
2. `panduan-P1-scaffold-ui.md` — P1.
3. `panduan-P2-dungeon.md` — P2.
4. `panduan-P3-battle-player.md` — P3.
5. `panduan-P4-gacha-inventory.md` — P4.
6. `panduan-P5-shop-storage.md` — P5.

## Pembagian

| Orang | Peran | Modul |
| --- | --- | --- |
| P1 | Scaffold, UI lib, platform, integrator | Makefile, `src/ui`, `src/platform`, `src/util`, `main.c` |
| P2 | Dungeon | `src/dungeon` |
| P3 | Battle dan player | `src/player`, `src/battle` |
| P4 | Gacha dan inventory | `src/gacha`, `src/inventory` |
| P5 | Shop, storage, leaderboard | `src/shop`, `src/storage` |

P3, P4, dan P5 hanya memakai UI lib dari P1. Mereka tidak menyentuh terminal,
ANSI, `printf` layar, atau `ui.c`.

## Urutan pengerjaan

1. P1 menyiapkan repo dan tag `contract-v1`.
2. P1 memberi tag `ui-ready`.
3. P2-P5 bekerja paralel di branch masing-masing.
4. P1 menggabungkan modul ke `dev`.
5. Semua orang menjalankan `make test` dan demo.
6. P1 menjalankan paritas dan menutup dokumentasi.

## Sebelum mulai

Cek alat di terminal. Jalankan satu per satu, jangan sekaligus:

```sh
git --version
gcc --version
make --version
sh --version
```

Expected: keempatnya mencetak versi.

Kalau ada yang menjawab `command not found`:

1. Jangan lanjut.
2. Buka `panduan-0-git-dan-kompilasi.md`.
3. Cari bagian **Kalau alat belum ada**.
4. Ikuti solusi untuk alat yang hilang.
5. Tutup terminal, buka lagi, cek ulang.

Kalau semua alat ada, lanjut membaca panduan peran.

## Istilah singkat

| Istilah | Arti sederhana |
| --- | --- |
| repo | folder project yang dilacak Git |
| branch | salinan kerja untuk satu tugas |
| commit | menyimpan perubahan ke riwayat Git |
| push | mengirim commit ke GitHub |
| build | mengubah kode menjadi program |
| test | menjalankan pemeriksaan otomatis |
| modul | folder/file untuk satu fitur |

## Kalau bingung

Ikuti aturan 30 menit:

1. Baca ulang langkah dan **Expected**.
2. Coba solusi di bagian **Kalau error** pada panduan peran.
3. Kalau masih macet, tanya P1 atau pemilik modul.
4. Kirim pesan berisi:
   - perintah yang dijalankan,
   - output lengkap dari terminal,
   - langkah yang sudah dicoba,
   - nama file yang sedang diedit.

Jangan mengirim "tidak bisa" tanpa output. Itu membuat penolong menebak.

## Aturan bukti

Setiap langkah dianggap selesai hanya jika ada bukti:

- perintah yang dijalankan,
- output yang muncul,
- test yang lulus,
- layar yang terlihat.

Jangan menulis "sudah selesai" tanpa salah satu bukti di atas.
