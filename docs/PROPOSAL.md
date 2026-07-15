# Proposal Mini Capstone Project

*Teori Bahasa dan Otomata — Semester IV, T.A. 2025/2026 Genap*

## "Otomatika": Aplikasi Web Analisis dan Transformasi Bahasa Formal pada Ekspresi Aritmatika

| | |
|---|---|
| **Nama** | Aulia Nazwa Huriah |
| **NIM** | 301240010 |
| **Kelas / Semester** | 4B / IV |
| **Judul Proyek** | Otomatika: Aplikasi Web Analisis dan Transformasi Bahasa Formal pada Ekspresi Aritmatika |
| **Repositori GitHub** | [github.com/Alnazh/tbo-capstone-301240010](https://github.com/Alnazh/tbo-capstone-301240010) |
| **Domain** | [https://www.301240010.my.id/](https://www.301240010.my.id/) |

---

## 1. Latar Belakang dan Tujuan

Teori Bahasa dan Otomata menyediakan fondasi formal untuk memahami bagaimana suatu
mesin abstrak dapat mengenali, memvalidasi, dan menganalisis struktur suatu bahasa.
Analisis ekspresi aritmatika dipilih sebagai studi kasus karena domain ini secara
alami membutuhkan keempat pilar teori bahasa formal sekaligus, mulai dari pengenalan
token melalui automata hingga hierarki tata bahasa, sehingga merefleksikan alur nyata
tahap awal sebuah compiler.

Proyek ini bertujuan merancang dan membangun aplikasi web bernama Otomatika yang
mendemonstrasikan proses tersebut secara end-to-end melalui empat modul yang saling
terhubung dalam satu narasi teknis: (1) tokenisasi dan pengenalan pola menggunakan
Finite State Automata dan Regular Expression, (2) penguraian struktur menggunakan
Pushdown Automata berbasis Context-Free Grammar, serta (3) transformasi tata bahasa
ke dalam Chomsky Normal Form. Seluruh algoritma inti (automata, mesin regex, parser,
CYK, konversi CNF/GNF) ditulis manual tanpa mengandalkan modul siap pakai seperti
`re` bawaan Python, agar benar-benar mendemonstrasikan konsep otomata yang dipelajari.

## 2. Ruang Lingkup

- Aplikasi memproses ekspresi aritmatika dengan operator `+`, `-`, `*` (kali), `/`
  (bagi), tanda kurung, serta bilangan bulat maupun desimal.
- Keempat modul wajib (FSA, Regular Expression, PDA/CFG, dan Hierarki Chomsky & CNF)
  diimplementasikan dalam satu aplikasi Flask yang saling terintegrasi melalui
  halaman beranda dan alur pipeline yang sama, bukan empat aplikasi terpisah.
- Setiap modul menyediakan input pengguna, proses simulasi/transformasi, serta output
  dan visualisasi SVG yang informatif sesuai spesifikasi tugas.
- Sebagai nilai tambah, disediakan simulator DFA/NFA kustom, konversi NFA ke DFA,
  simulator Moore/Mealy Machine, PDA generik untuk CFG bebas pengguna dengan
  pengujian keanggotaan CYK, serta konversi ke Greibach Normal Form.

## 3. Rancangan Sistem per Modul

### 3.1 Modul Finite State Automata (FSA)

Modul ini membangun sebuah DFA tokenizer dengan strategi *maximal munch* yang
mengubah karakter ekspresi menjadi deretan token (NUMBER, PLUS, MINUS, STAR, SLASH,
LPAREN, RPAREN), lengkap dengan visualisasi diagram state dan jejak transisi per
token dalam bentuk stepper animasi. Selain tokenizer bawaan, modul ini juga
menyediakan simulator DFA/NFA kustom di mana pengguna dapat mendefinisikan mesin
sendiri melalui format teks dan menguji string apa pun, dengan tipe mesin terdeteksi
otomatis.

Fitur konversi NFA ke DFA (*subset construction*) ditampilkan lengkap dengan tabel
langkah dan diagram sebelum/sesudah, termasuk contoh NFA dengan transisi-epsilon.
Sebagai fitur tambahan, modul ini menyediakan simulator Moore Machine dan Mealy
Machine sederhana.

### 3.2 Modul Regular Expression (RE)

Modul ini merupakan mesin regex buatan sendiri (bukan modul `re` bawaan Python) yang
bekerja melalui tiga tahap: parser ekspresi regular, konstruksi Thompson menjadi NFA,
dan subset construction menjadi DFA. Mesin ini mendukung union (`|`), star (`*`),
plus (`+`), opsional (`?`), grup (`()`), character class (`[a-z0-9]`), serta
shorthand `\d`, `\w`, `\s`.

Sistem menampilkan tata bahasa reguler (linear kanan) yang ekuivalen dengan DFA hasil
kompilasi, misalnya untuk pola bilangan bulat `digit digit*`, serta menyediakan uji
pencocokan string dengan visualisasi jejak state per karakter.

### 3.3 Modul Pushdown Automata & CFG

Modul ini mem-parsing ekspresi aritmatika berdasarkan grammar standar
`E → E + T | E − T | T`, `T → T × F | T ÷ F | F`, `F → ( E ) | bilangan`, menggunakan
teknik *precedence climbing*. Untuk suatu input, misalnya `(2+3)*4`, sistem
menghasilkan pohon penurunan, derivasi kiri dan kanan, serta simulasi stack PDA
(shift-reduce) langkah demi langkah, di mana stack berperan memverifikasi kesesuaian
pasangan tanda kurung bersarang.

Sebagai pengembangan lanjutan, disediakan PDA generik yang menerima CFG bebas yang
didefinisikan pengguna. Grammar tersebut otomatis dikonversi ke Chomsky Normal Form,
lalu diuji keanggotaannya dengan algoritma CYK; apabila string diterima, pohon
penurunan dan jejak stack direkonstruksi dari hasil tabel CYK.

### 3.4 Modul Hierarki Chomsky & Chomsky Normal Form

Modul ini menampilkan panel edukatif mengenai hierarki Chomsky (Tipe 0–3) dan
kaitannya dengan tiap modul sebelumnya, serta konversi CFG sembarang (termasuk
grammar pada modul 3.3) menjadi Chomsky Normal Form. Setiap langkah transformasi
ditampilkan secara eksplisit: penetapan simbol START, eliminasi ε/nullable, eliminasi
unit production, eliminasi simbol useless, hingga pemecahan produksi menjadi bentuk
TERM dan BIN.

Sebagai fitur tambahan, disediakan konversi ke Greibach Normal Form yang bersifat
eksperimental untuk grammar kompleks; apabila konversi gagal, aplikasi akan
menampilkan pesan yang jujur alih-alih hasil yang keliru.

## 4. Arsitektur dan Tech Stack

Aplikasi dibangun sebagai satu aplikasi Flask dengan halaman beranda (pipeline demo
dan navigasi) serta empat route independen untuk tiap modul (`/tokenizer`, `/regex`,
`/parser`, `/cnf`) yang berbagi layout dasar (navbar dan footer) yang sama, sehingga
antarmuka konsisten di perangkat desktop maupun mobile. Interaksi modul dengan
backend dilakukan melalui endpoint API (mis. `/api/tokenize`, `/api/fsa/simulate`,
`/api/regex/compile`, `/api/cfg/cnf`) yang dipanggil secara asinkron oleh JavaScript
vanilla di sisi klien.

Seluruh logika inti (automata, regex engine, parser, CYK, konversi CNF/GNF) berada
pada `app.py` yang disusun berurutan dalam lima bagian mengikuti urutan modul,
ditutup bagian routing Flask, sehingga tetap terstruktur meski berada dalam satu
berkas.

| Komponen | Teknologi |
|---|---|
| Backend | Python 3 + Flask (satu aplikasi web, seluruh logika inti pada `app.py`) |
| Frontend | HTML5, CSS3 murni dengan grid/utilitas layout buatan sendiri (tanpa Bootstrap/CDN), JavaScript vanilla tanpa framework |
| Visualisasi | SVG digambar dinamis di sisi klien untuk diagram state, pohon penurunan, dan tabel CYK, tanpa library diagram eksternal |
| Pengujian | `unittest` Python (41 kasus uji backend) dan regresi logika frontend murni via Node `vm` |
| Version Control | Git & GitHub, repositori publik dengan commit bertahap per modul |
| Hosting | Railway/Render (auto-detect `requirements.txt` & `Procfile`) atau VPS dengan gunicorn + Nginx, dihubungkan ke domain `.my.id` dengan HTTPS aktif |

## 5. Rencana Deploy dan Repositori

- Domain didaftarkan melalui layanan `.my.id` (mis. is.my.id), lalu diarahkan ke
  layanan hosting yang mendukung proses Python seperti Railway atau Render, dengan
  HTTPS aktif dan redirect otomatis dari HTTP ke HTTPS.
- Sebagai alternatif, aplikasi dapat dideploy pada VPS menggunakan gunicorn di
  belakang Nginx sebagai reverse proxy, dengan sertifikat HTTPS dari Let's Encrypt
  (certbot).
- Repositori GitHub bersifat publik dengan struktur folder `templates/` (halaman per
  modul), `static/` (CSS dan JavaScript), `tests/` (kasus uji backend), `tests_js/`
  (regresi logika frontend), dan `docs/` (proposal serta draf laporan).
- README.md memuat deskripsi proyek, daftar fitur tiap modul, tech stack, instruksi
  instalasi lokal, tautan domain aktif, dan tautan video demo YouTube. Domain
  dipastikan aktif tanpa login dan bertahan minimal dua minggu setelah batas waktu
  penilaian.

## 6. Rencana Pengujian

Pengujian backend menggunakan `unittest` Python dengan 41 kasus uji
(`tests/test_app.py`) yang mencakup simulasi DFA/NFA dan konversi NFA ke DFA, mesin
regex (parser, Thompson construction, subset construction), parser ekspresi
aritmatika dan PDA generik, algoritma CYK, serta konversi CNF dan GNF. Pengujian
logika frontend murni dilakukan melalui Node `vm` (`tests_js/run.js`) untuk
memastikan konsistensi hasil antara sisi klien dan backend.

Kasus uji mencakup input valid, input tidak valid, dan edge case seperti string
kosong, tanda kurung tidak seimbang, ekspresi bersarang dalam, serta grammar dengan
ε-production untuk menguji ketahanan proses transformasi CNF.
