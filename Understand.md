#design-sprint

[[Fitur]]

Test pull on mobile

## Masalah / Goal
### Context
Instansi pemerintah mempunyai sistem cuti, dimana PNS bisa meminta cuti dengan izin tertentu seperti [[Persyaratan Cuti]]. Sistem dilakukan denngan 
1. PNS membuat surat cuti, 
2. petugas yang bersangkutan jumlah [[Persyaratan Cuti#Jatah cuti]] yang tersedia dari si PNS, 
3. PNS memberikan data untuk [[Persyaratan Cuti#Kriteria persyaratan cuti]]
4. Atasan dari instansi tempat PNS bekerja memberikan persetujuan
5. dan Pejabat yang bersangkutan memberikan persetujuan

Proses ini dilakukan dengan cara semi manual, dimana ada aplikasi yang bisa menangani hal tersebut, tetapi sistem masih harus dilakukan dengan menuliskan kebutuhan form secara manual dan mencari data yang ada pada aplikasi. Ini merupakan salah satu masalah yang akan ditangani dengan membuat aplikasi khusus sehingga
1. Entry data form bisa dilakukan secara otomatis
2. Kemudahan penandatanganan form cuti untuk persetujuan
3. Mempercepat alur proses

Kenapa mempercepat alur proses? Dalam proses persetujuan form cuti, PNS harus memberikan [[Persyaratan Cuti]] berupa file, dokumen, atau surat. Dokumen tersebut harus memelalui proses verifikasi secara manual dengan melihat secara satu-persatu. Membuat proses persetujuan form cuti menjadi sangat lama dan melelahkan petugas/atasan/pejabat yang bersangkutan. Proses ini nantinya akan dilakukan secara otomatis oleh mesin/aplikasi dengan bantuan artificial intelligence dan pengolahan data citra pada surat yang diberikan, tentunya hasil verifikasi akan bisa dikoreksi oleh petugas dan tidak akan menjadi verifikasi final.

### Poin masalah
1. Proses lama
2. Proses dilakukan secara semi manual
3. Pemeriksaan dokumen dilakukan secara manual

***
## Ekstrak Masalah
1. Entry data form tidak dilakukan secara otomatis
2. Penghitungan jatah cuti dilakukan dengan cara semi manual
3. Verifikasi dokumen dilakukan secara manual
4. Penandatangan form oleh pejabat dan atasan yang lama

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

#### 4. Tanda tangan otomatis
Penandatangan akan dilakukan secara otomatis dengan beberapa pilihan cara
- Sistem menyimpan tandatangan sehingga bisa digunakan setiap kali form cuti disetujui
- Sistem meminta tanda tangan melalui file atau tanda tangan secara langsung melalui aplikasi

***
## Potensi masalah
1. Menyimpan tanda tangan pada sistem yang tidak aman bisa membuat tanda tangan diambil ketika terjadi pembobolan sistem dan membuat tanda tangan atasan/pejabat berada di tangan orang yang salah, sehingga bisa digunakan untuk tindakan yang melanggar hukum
2. Pengolahan data citra memerlukan data yang cukup besar sehingga memerlukan penyimpanan yang banyak
3. Penggunaan python dan django memerlukan hosting yang mendukung teknologi ini
4. Penyimpanan data PNS pada sistem yang tidak aman sangat tidak dianjurkan dan lebih baik mengambil data dari API, jika ada

