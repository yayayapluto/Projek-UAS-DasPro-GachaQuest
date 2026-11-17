# Projek UAS DasPro — Gacha Quest (Starter Kit)

Starter kit ini berisi panduan pembagian kerja untuk lima orang. Isinya bukan
kode jadi, bukan jawaban, dan tidak bisa langsung dijalankan. Tujuannya agar
kelompok bisa membangun project dari nol sampai setara repo referensi.

Repo referensi (hanya dibaca):
`D:/Kuliah/dasar_pemrograman/projek uas`.

## Mulai dari sini

Baca berurutan:

1. `docs/panduan-5-orang.md` — indeks dan pembagian peran.
2. `docs/rencana-pembagian-tugas-5-orang.md` — target, fase, gate.
3. `docs/panduan-0-git-dan-kompilasi.md` — git, branch, konflik, `make`.
4. Panduan peran:
   - `docs/panduan-P1-scaffold-ui.md`
   - `docs/panduan-P2-dungeon.md`
   - `docs/panduan-P3-battle-player.md`
   - `docs/panduan-P4-gacha-inventory.md`
   - `docs/panduan-P5-shop-storage.md`

## Prasyarat

- Git for Windows.
- MSYS2 dengan `gcc`, GNU `make`, dan `sh`.
- `C:\msys64\usr\bin` masuk `PATH`.
- Windows Terminal, PowerShell, atau CMD untuk menjalankan game.

## Aturan

- Panduan tidak memuat kode solusi. Peserta menulis implementasi sendiri.
- Kontrak berupa header, data katalog, fixture input, dan driver uji disalin
  dari repo referensi saat Fase 0 pekerjaan.
- Repo referensi tidak boleh diubah.
- P3, P4, dan P5 hanya memakai UI lib dari P1. Mereka tidak menyentuh terminal,
  ANSI, atau `printf` layar.
- Setiap langkah selesai hanya jika punya bukti: perintah, output, test lulus,
  atau layar yang terlihat.

## Hasil akhir

Project baru yang:

- kompilasi tanpa warning,
- `make test` lulus,
- seluruh layar dan alur demo berjalan,
- output skenario pipa setara repo referensi.

## Struktur

```text
Projek-UAS-DasPro-GachaQuest/
├── README.md
├── .gitignore
└── docs/
    ├── rencana-pembagian-tugas-5-orang.md
    ├── panduan-5-orang.md
    ├── panduan-0-git-dan-kompilasi.md
    ├── panduan-P1-scaffold-ui.md
    ├── panduan-P2-dungeon.md
    ├── panduan-P3-battle-player.md
    ├── panduan-P4-gacha-inventory.md
    └── panduan-P5-shop-storage.md
```

Starter kit sengaja tidak berisi `.c`, `.h`, `Makefile`, data, atau test.
