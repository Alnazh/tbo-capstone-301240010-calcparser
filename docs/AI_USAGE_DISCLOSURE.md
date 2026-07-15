# Disclosure Penggunaan AI Generatif

Sesuai ketentuan integritas akademik pada dokumen tugas, bagian ini mengungkapkan
secara jujur penggunaan alat bantu AI generatif selama pengerjaan Capstone Project ini.

## Tools yang Digunakan

Asisten AI generatif Claude (Anthropic) digunakan sebagai alat bantu selama
pengerjaan, baik pada tahap coding maupun penyusunan laporan, sesuai batas yang
diperbolehkan pada ketentuan tugas, yaitu AI sebagai alat bantu dan bukan pengganti
proses belajar mahasiswa. Porsi penggunaan AI diperkirakan sekitar separuh dari
keseluruhan proses pengerjaan, sedangkan separuh lainnya dikerjakan, diperiksa ulang,
dan dimodifikasi secara mandiri oleh mahasiswa.

## Bagian yang Dibantu AI

1. Draf awal kerangka kode untuk beberapa fungsi inti, seperti struktur dasar
   `epsilon_closure` dan pola umum Thompson Construction, yang selanjutnya
   disesuaikan agar konsisten dengan
   gaya kode di seluruh proyek.
2. Bantuan menemukan penyebab error saat proses debugging, terutama pada tahap
   awal implementasi konversi CNF.
3. Draf awal beberapa paragraf teori di Bab II sebagai bahan acuan, yang kemudian
   ditulis ulang dengan kalimat sendiri agar tidak menjiplak sumber aslinya.
4. Ide awal tata letak visualisasi SVG, seperti diagram transisi dan pohon
   penurunan, sebelum akhirnya diubah proporsi dan detailnya sesuai kebutuhan
   aplikasi.

## Bagian yang TIDAK Dibantu AI

1. Penulisan ulang dan penyesuaian nama variabel, struktur fungsi, serta sebagian
   alur logika pada beberapa modul agar sesuai pemahaman sendiri, termasuk
   penyesuaian pada tahapan `cnf_step_remove_unit` dan parser precedence climbing.
2. Instalasi, menjalankan, dan memverifikasi aplikasi secara langsung di komputer
   sendiri, termasuk menjalankan seluruh 41 test case backend dan 9 test regresi
   frontend satu per satu untuk memastikan hasilnya benar.
3. Proses deployment ke domain publik (registrasi domain, konfigurasi CNAME,
   aktivasi HTTPS) serta pengelolaan repositori GitHub dengan commit bertahap per
   modul.
4. Penelusuran kode program baris demi baris untuk memahami alur tiap algoritma,
   sekaligus memperbaiki bagian yang dirasa kurang sesuai dengan pemahaman sendiri.
5. Penulisan seluruh analisis, evaluasi kritis, kesimpulan, dan refleksi
   pembelajaran pada laporan berdasarkan hasil pengujian yang telah dijalankan
   sendiri.

## Pemahaman dan Modifikasi Mahasiswa

Karena sebagian kode disusun dengan bantuan AI pada tahap awal, maka dilakukan
proses mempelajari ulang dan memodifikasi kembali kode tersebut agar benar-benar
dipahami, mulai dari menelusuri baris demi baris tiap fungsi kunci, mengganti
sebagian penamaan variabel dan struktur agar lebih mudah dipahami sendiri, hingga
mencocokkan kembali setiap langkah algoritma dengan definisi formal (Q, Σ, δ, q0, F)
yang dipelajari pada mata kuliah. Proses inilah yang membuat sebagian kode akhir
berbeda dari draf awal yang dibantu AI. Mahasiswa bertanggung jawab penuh atas
kebenaran dan pemahaman yang dituangkan dalam laporan ini, sejalan dengan ketentuan
bahwa AI generatif digunakan sebagai alat bantu dan bukan pengganti proses belajar.

---

Kode program lengkap (termasuk implementasi seluruh algoritma inti seperti
`epsilon_closure`, Thompson Construction, precedence climbing, algoritma CYK, dan
konversi CNF/GNF) tersedia pada repositori GitHub: <https://github.com/Alnazh/tbo-capstone-301240010>
