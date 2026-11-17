# Panduan 0 — Git dan Kompilasi

Berlaku untuk semua anggota. Rencana induk:
`rencana-pembagian-tugas-5-orang.md`.

Panduan ini ditulis untuk orang yang belum pernah memakai Git atau compiler.
Setiap perintah dijelaskan: apa yang diketik, output normalnya apa, dan apa yang
harus dilakukan kalau outputnya berbeda.

## Cara membaca panduan

1. Buka terminal di folder kerja.
2. Ketik satu perintah, tekan Enter.
3. Bandingkan output dengan bagian **Expected**.
4. Kalau sama, lanjut. Kalau berbeda, baca **Kalau error**.
5. Jangan lanjut ke langkah berikutnya kalau langkah sekarang belum benar.

Jangan menyalin semua perintah sekaligus. Satu perintah, satu pemeriksaan.

## Cek alat

Buka PowerShell, CMD, atau Windows Terminal. Ketik satu per satu:

```sh
git --version
```

Expected:

```text
git version 2.x.x.windows.x
```

```sh
gcc --version
```

Expected:

```text
gcc (Rev...) ...
```

```sh
make --version
```

Expected:

```text
GNU Make 4.x
```

```sh
sh --version
```

Expected:

```text
GNU bash, version ...
```

Kalau keempatnya mencetak versi, lanjut ke **Setup repo baru**.

## Kalau alat belum ada

Jangan menebak. Cek satu per satu. Setelah memasang, **tutup terminal lalu buka
terminal baru**, karena `PATH` lama tidak berubah.

### `git` tidak ditemukan

Gejala:

```text
git : The term 'git' is not recognized...
```

atau:

```text
'git' is not recognized as an internal or external command
```

Solusi:

1. Unduh Git for Windows dari `https://git-scm.com/download/win`.
2. Jalankan installer, pilih opsi default.
3. Setelah selesai, tutup semua terminal.
4. Buka PowerShell baru.
5. Jalankan `git --version` lagi.

Kalau masih gagal, cek `PATH` Windows:

1. Tekan `Win + R`, ketik `sysdm.cpl`, Enter.
2. Buka tab **Advanced** → **Environment Variables**.
3. Di **User variables**, pilih `Path` → **Edit**.
4. Pastikan ada `C:\Program Files\Git\cmd`.
5. Kalau belum ada, klik **New**, isi path itu, lalu OK.
6. Tutup dan buka ulang terminal.

### `gcc` tidak ditemukan

Gejala:

```text
gcc : The term 'gcc' is not recognized...
```

atau:

```text
make: cc: Command not found
```

Solusi:

1. Unduh dan pasang MSYS2 dari `https://www.msys2.org/`.
2. Gunakan lokasi default `C:\msys64`.
3. Buka **MSYS2 UCRT64** dari Start Menu.
4. Jalankan:

```sh
pacman -Syu
```

5. Kalau diminta menutup jendela, tutup, lalu buka **MSYS2 UCRT64** lagi.
6. Jalankan:

```sh
pacman -S --needed base-devel mingw-w64-ucrt-x86_64-gcc
```

7. Ketik `Y` kalau diminta konfirmasi.
8. Tutup MSYS2.
9. Tambahkan `C:\msys64\usr\bin` dan `C:\msys64\ucrt64\bin` ke `PATH`
   Windows dengan cara yang sama seperti langkah Git.
10. Buka PowerShell baru, jalankan `gcc --version`.

Kalau `gcc` hanya jalan di jendela MSYS2 tetapi tidak di PowerShell, berarti
`PATH` Windows belum benar. Ulangi langkah 9.

### `make` tidak ditemukan

Gejala:

```text
make : The term 'make' is not recognized...
```

Solusi:

1. Buka **MSYS2 UCRT64**.
2. Jalankan:

```sh
pacman -S --needed make
```

3. Pastikan `C:\msys64\usr\bin` ada di `PATH` Windows.
4. Tutup dan buka ulang terminal.
5. Jalankan `make --version`.

Kalau `make` ada di MSYS2 tetapi tidak di PowerShell, masalahnya `PATH`, bukan
instalasi.

### `sh` tidak ditemukan

Gejala:

```text
sh : The term 'sh' is not recognized...
```

Solusi:

1. Pastikan MSYS2 sudah terpasang.
2. Tambahkan `C:\msys64\usr\bin` ke `PATH` Windows.
3. Tutup dan buka ulang terminal.
4. Jalankan `sh --version`.

`sh` dipakai `make test` dan `tests/run_tests.sh`. Tanpa `sh`, build bisa jalan
tetapi test tidak.

### `pacman` tidak ditemukan

Gejala:

```text
pacman : The term 'pacman' is not recognized...
```

Artinya kamu menjalankan perintah MSYS2 dari PowerShell. `pacman` hanya ada di
dalam jendela MSYS2. Buka **MSYS2 UCRT64** dari Start Menu, lalu jalankan
`pacman` di sana.

## Setup repo baru

1. Buat folder kerja.
2. Masuk ke folder.
3. Inisialisasi Git.
4. Buat branch `main`.
5. Buat branch kerja `feat/scaffold`.

```sh
mkdir Projek-UAS-DasPro-GachaQuest
cd Projek-UAS-DasPro-GachaQuest
git init
git branch -M main
git checkout -b feat/scaffold
```

Expected:

```text
Initialized empty Git repository in .../Projek-UAS-DasPro-GachaQuest/.git/
```

Cek branch:

```sh
git branch --show-current
```

Expected:

```text
feat/scaffold
```

Kalau error:

- `fatal: not a git repository` → kamu belum ada di folder repo. Jalankan
  `pwd` lalu `cd` ke folder yang benar.
- `fatal: a branch named 'feat/scaffold' already exists` → branch sudah ada.
  Jalankan `git checkout feat/scaffold`.
- `fatal: not a valid object name: 'main'` → belum ada commit. Buat commit
  pertama dulu.

## Identitas commit

Sekali per komputer:

```sh
git config --global user.name "Nama Kamu"
git config --global user.email "email@contoh.com"
```

Cek:

```sh
git config --global --list
```

Expected: ada baris `user.name=...` dan `user.email=...`.

Kalau `git commit` menolak dengan pesan `Please tell me who you are`, jalankan
dua perintah di atas, lalu commit lagi.

## Alur harian

Kerjakan dari branch sendiri, bukan `main`.

```sh
git checkout main
git pull
git checkout feat/nama-modul
git rebase main
```

Expected: tidak ada konflik. Kalau ada konflik, selesaikan dulu sebelum
mengubah kode. Langkahnya ada di bagian **Konflik**.

Kalau `git pull` gagal karena belum ada remote:

```text
fatal: No remote repository specified...
```

Itu normal untuk repo lokal baru. Lanjutkan pekerjaan; remote dibuat P1.

Sebelum commit, lihat apa yang berubah:

```sh
git status
git diff
```

Expected:

- `git status` menampilkan file yang berubah.
- `git diff` menampilkan isi perubahan.

Kalau `git status` bersih tetapi kamu merasa sudah mengubah file, berarti file
tersimpan di folder lain. Cek `pwd`.

Commit:

```sh
git add path/file-yang-berubah
git commit -m "feat(dungeon): tambah gerak dan kamera"
```

Expected:

```text
[feat/dungeon 1a2b3c4] feat(dungeon): tambah gerak dan kamera
 3 files changed, ...
```

Kalau error:

- `nothing to commit` → tidak ada perubahan yang ditambahkan. Cek `git status`.
- `pathspec ... did not match` → path file salah. Salin path dari `git status`.
- `Please tell me who you are` → isi identitas Git.

Push:

```sh
git push -u origin feat/nama-modul
```

Expected: branch baru muncul di remote.

Kalau error:

- `remote origin already exists` → remote sudah ada. Jalankan
  `git remote -v` untuk melihat.
- `Authentication failed` → login GitHub belum benar. Jalankan
  `gh auth login` atau login lewat Git Credential Manager.
- `Updates were rejected` → remote punya commit yang belum kamu punya.
  Jalankan `git pull --rebase`, selesaikan konflik, lalu push lagi.

## Aturan branch

| Branch | Pemilik | Isi |
| --- | --- | --- |
| `main` | P1 | hasil stabil, hanya menerima merge |
| `feat/scaffold` | P1 | repo, Makefile, kontrak |
| `feat/ui` | P1 | UI lib dan preview |
| `feat/platform` | P1 | util dan platform |
| `feat/main-integration` | P1 | main dan hub |
| `feat/dungeon` | P2 | dungeon |
| `feat/player-battle` | P3 | player dan battle |
| `feat/gacha-inventory` | P4 | gacha dan inventory |
| `feat/shop-storage` | P5 | shop dan storage |

Branch dibuat dari tag `contract-v1`, kecuali branch integrasi P1.

```sh
git checkout -b feat/dungeon contract-v1
```

Expected:

```text
Switched to a new branch 'feat/dungeon'
```

Kalau error `fatal: invalid reference: contract-v1`, tag belum dibuat. Tunggu
P1, jangan membuat tag sendiri.

## Urutan merge

1. `feat/scaffold` → `main`, tag `contract-v1`.
2. `feat/ui` → `main`, tag `ui-ready`.
3. `feat/player-battle` → `dev`.
4. `feat/gacha-inventory` → `dev`.
5. `feat/shop-storage` → `dev`.
6. `feat/dungeon` → `dev`.
7. `feat/main-integration` → `dev`.
8. `dev` diuji penuh, lalu merge ke `main`.

## Konflik

Jika `git rebase` berhenti:

```sh
git status
```

Expected: daftar file konflik dengan status `both modified`.

Aturan:

- File milikmu: perbaiki sendiri.
- File milik orang lain: jangan menimpa. Hubungi pemiliknya.
- Header bersama: P1 yang memutuskan.
- Setelah selesai:

```sh
git add file-yang-sudah-diperbaiki
git rebase --continue
```

Jika salah dan ingin membatalkan rebase:

```sh
git rebase --abort
```

Expected: kembali ke kondisi sebelum rebase.

Kalau bingung melihat tanda konflik:

```text
<<<<<<< HEAD
kode kamu
=======
kode orang lain
>>>>>>> nama-branch
```

Jangan menghapus keduanya tanpa membaca. Pilih atau gabungkan dengan benar,
lalu hapus tiga penanda itu.

## Review

Sebelum minta review:

```sh
make
make test
```

Expected: build tanpa warning, test `0 gagal`.

Yang dicek reviewer:

- Hanya file milik pemohon yang berubah.
- Tidak ada `printf` layar atau akses terminal langsung di modul pemula.
- Tidak ada `rand()` di luar modul RNG.
- Test tidak dilemahkan.
- Teks pemain tidak berubah.

## Tag

Tag hanya dibuat P1 setelah gate lulus.

```sh
git tag contract-v1
git tag ui-ready
git tag
```

Expected:

```text
contract-v1
ui-ready
```

Kalau tag sudah ada, `git tag` akan menolak. Jangan hapus tag lama tanpa
persetujuan P1.

## Kompilasi

Semua perintah dari root repo, tempat `Makefile` berada. Cek dulu:

```sh
pwd
ls Makefile
```

Expected: `Makefile` terlihat. Kalau tidak, kamu di folder yang salah.

### Build

```sh
make
```

Expected:

```text
gcc -std=c11 -Wall -Wextra -Wpedantic ... -o bin/game ...
# tidak ada warning
```

Kalau error:

- `make: *** No targets specified and no makefile found` → tidak ada
  `Makefile` di folder itu. `cd` ke root repo.
- `gcc: command not found` → `gcc` belum masuk `PATH`. Ulangi bagian
  **`gcc` tidak ditemukan**.
- `No such file or directory` → ada file yang belum dibuat. Baca nama file di
  pesan error; minta pemilik modul melengkapinya.
- `undefined reference to ...` → ada fungsi yang belum diimplementasi atau
  file `.c` belum masuk `Makefile`. Jangan mengubah `Makefile` sendiri kalau
  bukan P1.
- `warning:` → jangan diabaikan. Perbaiki file yang disebut.

### Jalankan

```sh
make start
```

Expected: game langsung berjalan dari `bin/game`.

Atau:

```sh
bin/game
```

Kalau `bin/game` tidak ada, build gagal. Baca error `make` dulu.

### Test

```sh
make test
```

Expected:

```text
=== Ringkasan: ... lulus, 0 gagal ===
```

Kalau ada `GAGAL`:

1. Baca nama driver dan file input yang disebut.
2. Jalankan driver itu sendiri, misalnya `bin/t_dungeon`.
3. Jangan mengubah test agar lulus. Perbaiki kode.
4. Kalau tidak paham, kirim potongan output ke pemilik modul.

Kalau `sh: command not found`, ulangi bagian **`sh` tidak ditemukan**.

### Debug sanitizer

```sh
make debug
```

Expected: build dan seluruh test berjalan dengan AddressSanitizer/UBSan,
tanpa laporan memory error.

Di Windows, target ini memakai clang64. Kalau gagal:

1. Cek `C:\msys64\clang64\bin\clang.exe` ada.
2. Kalau tidak ada, buka MSYS2 UCRT64 dan jalankan
   `pacman -S --needed mingw-w64-clang-x86_64-toolchain`.
3. Kalau masih gagal, lewati `make debug` dan pakai `make test`; jangan
   mengubah `CC_SAN` sendiri.

### Preview UI

```sh
make preview
```

Expected: `bin/ui_preview` tampil. Tekan Esc atau ikuti footer untuk keluar.

Kalau layar kosong:

- Jalankan dari Windows Terminal, bukan output yang di-pipe.
- Pastikan terminal minimal 50x20.
- Kalau masih kosong, laporkan ke P1 dengan nama terminal yang dipakai.

### Bersihkan

```sh
make clean
```

Expected: folder `bin/` hilang. Build berikutnya dari nol.

Kalau `Permission denied`, tutup game yang masih berjalan, lalu ulangi.

## Kalau bingung

Ikuti aturan 30 menit:

1. Baca ulang langkah dan **Expected**.
2. Coba solusi di bagian **Kalau error**.
3. Kalau masih macet, tanya pemilik modul atau P1.
4. Kirim: perintah yang dijalankan, output lengkap, dan langkah yang sudah
   dicoba. Jangan kirim "tidak bisa" saja.

## Aturan keselamatan git

Jangan jalankan tanpa tahu akibatnya:

```text
git reset --hard
git clean -fd
git push --force
```

Jika ragu, tanya P1. Simpan pekerjaan dengan commit kecil sebelum mencoba
perintah berisiko.
