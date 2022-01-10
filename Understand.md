#design-sprint

[[Fitur]]

Test pull on mobile

## Masalah / Goal
### Context
Instansi pemerintah mempunyai sistem cuti, dimana PNS bisa meminta cuti dengan izin tertentu seperti [[Persyaratan Cuti]]. Sistem dilakukan dengan 
1. PNS menghadap atasan untuk meminta persetujuan cuti 
2. PNS memberikan data untuk [[Persyaratan Cuti#Kriteria persyaratan cuti]] dan [[Persyaratan Cuti#Jatah cuti]] yang masih ia miliki
3. Atasan/Petugas yang berwenang di unit kerja mengisi [[Form Cuti]] sesuai dengan permintaan PNS dan mengvaluasi [[Persyaratan Cuti#Kriteria persyaratan cuti]] yang diberikan oleh PNS
4. Atasan dari instansi tempat PNS bekerja memberikan persetujuan
5. Pejabat memberikan form cuti yang telah disetujui dan berstempel
6. Pejabat yang bersangkutan memberikan persetujuan

Semau proses diatas dilakukan secara manual.

### Poin masalah
1. Proses pengisian form yang masih dilakukan secara manual
2. Verifikasi jatah cuti yang hanya bisa dikonfirmasi dari PNS yang bersangkutan
3. Verifikasi berkas yang dilakukan secara manual

***
## Solusi
#### 1. Entry data otomatis
Entry data form (seperti data diri pns) dilakukan secara otomatis sesuai dengan data dari akun yang sedang login atau dengan mengisikan NIP dari pns pada aplikasi petugas.

Data yang akan terisi otomatis berupa
1. Bondowoso, (tanggal) -> diambil dari tanggal permintaan (optional hanya admin)
2. Kepada Yth (nama atasan) -> atasan unit kerja PNS bekerja
3. Di (tempat instansi) -> Unit kerja
4. Data diri pegawai
5. Catatan cuti (berupa [[Persyaratan Cuti#Jatah cuti]])

Data diri yang diperlukan untuk form akan diambil secara langsung oleh mesin dari database dengan referensi NIP. Data yang disimpan berupa
- Nama
- Jabatan
- Unit kerja
- NIP
- Masa kerja (diambil dari tanggal sekarang - tanggal jadi PNS)

#### 2. Catatan jatah cuti
Penghitungan jatah cuti akan dilakukan dengan otomatis dengan menghitung data yang telah tersimpan pada database. Jatah merupakan jatah cuti dari PNS dari NIP yang sedang dipilih.

Penghitungan jatah cuti dilakukan dengan menyimpan 
1. Jenis cuti
2. NIP
3. Tanggal
Dan melakukan conditial formating seperti excel dengan menggunakan syarat [[Persyaratan Cuti#Jatah cuti]] 

#### 3. Verifikasi dokumen/surat
Verifikasi dokumen dilakukan secara otomatis dengan bantuan pengolahan data citra dan artificial intelligence yang akan dibangun dengan python. Verifikasi saat ini akan berfokus pada
- Surat Keterangan dokter yang mempunyai Izin praktek
- Surat keterangan dari Bidan
Dengan kriteria verifikasi pada [[Persyaratan Cuti#Kriteria persyaratan cuti]]

[[Cara & referensi jurnal verifikasi dokumen]]


***
## Potensi masalah
1. Menyimpan tanda tangan pada sistem yang tidak aman bisa membuat tanda tangan diambil ketika terjadi pembobolan sistem dan membuat tanda tangan atasan/pejabat berada di tangan orang yang salah, sehingga bisa digunakan untuk tindakan yang melanggar hukum
2. Pengolahan data citra memerlukan data yang cukup besar sehingga memerlukan penyimpanan yang banyak
3. Penggunaan python dan django memerlukan hosting yang mendukung teknologi ini
4. Penyimpanan data PNS pada sistem yang tidak aman sangat tidak dianjurkan dan lebih baik mengambil data dari API, jika ada


# Alur pengajuan di aplikasi
1. PNS mengajukan cuti kepada atasan atau bagian kepegawaian pada unit kerja tempat ia bekerja
2. PNS menyerahkan [[Persyaratan Cuti]]
3. Bagian kepegawaian atau atasan mengisi form cuti miliki PNS
4. Aplikasi menghitung jumlah cuti yang diambil
5. Bagian kepegawaian atau atasan memasukkan scan persyaratan cuti yang diberikan
6. Aplikasi akan melakukan verifikasi pada scan persyaratan cuti yang telah dimasukkan
7. Setelah persyaratan telah diverifikasi
8. Bagian kepegawaian atau atasan mencetak form cuti 
9. Form cuti kemudian ditanda tangani dan diberikan stempel
10. Scan form cuti yang telah berstempel dimasukkan kembali kedalam aplikasi untuk dilihat oleh pejabat yang bersangkutan
11. Pejabat melakukan persetujuan pada form cuti yang telah berstempel dan persyaratan cuti  