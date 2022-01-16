#design-sprint 

Yang harus dilakukan hari ini
- [x] Memecah solusi atau masalah menjadi beberapa bagian kecil
- [x] Membuat wireframe aplikasi

## Memecah solusi
[[Understand#Solusi]]

Disini akan dijabarkan lebih detail lagi bagaimana caranya

### 1. Entry data otomatis

Selain memasukkan data pada database, aplikasi diharuskan melakukan print data sesuai dengan format form yang ada. Format form adalah sebagai berikut

![[IMG_20220111_080822.jpg]]

Aplikasi harus menargetkan setiap kolom yang ada. Tugas dari module ini adalah
1. Melakukan editing pada file docx yang sudah tersedia
2. Print file docx yang telah dilakukan editing

Untuk melakukan editing, setiap kolom yang harus diisi oleh aplikasi akan diberikan sebuah text/label yang bisa dikenali oleh aplikasi, kemudian mengganti text tersebut dengan data yang dimasukkan oleh atasan atau badan kepegawaiain. Proses persiapan adalah
1. Siapkan file form-cuti.docx
2. Beri setiap kolom yang akan diisi oleh aplikasi dengan label, label harus unique

Setelah data telah siap, module [python-docx](https://python-docx.readthedocs.io/en/latest/) akan digunakan untuk merubah setiap label tersebut dengan data yang dimasukkan oleh atasan atau badan kepegawaian.

Untuk melakukan print ada beberapa solusi untuk melakukan print
1. Menggunakan sistem dengan python, berdasarkan [referensi](https://stackoverflow.com/questions/12723818/print-to-standard-printer-from-python) dengan nilai plus bisa dilakukan melalui OS berbeda dan nilai minus kurangnya pilihan print untuk print seperti memilih printer dan keharusan untuk memeriksa sistem operasi.
2. Menggunakan module [doc2pdf](https://pypi.org/project/docx2pdf/) dengan syarat sistem operasi harus memiliki aplikasi ms word, syaratnya sangat mudah, tetapi karena aplikasi akan dijalankan diserver kemungkinan akan tidak bisa diterapkan.
> Cara diatas harus dilakukan dengan menambah fitur setting printer
3. Manual print, aplikasi akan mengirimkan file docx yang sudah diproses ke dalam folder download dan membiarkan pengguna membuka file kemudian melakukan print seperti biasanya. Dimana agak ribet, buang-buang tenaga dan kurang profesional.

> Revisi proses Print

Langkah print tidak dilakukan dengan mengubah document .docx melainkan membuat tampilan form cuti dengan html dan css, kemudian melakukan print menggunakan browser. Dengan begini langkah persiapan print menjadi 
1. Buat HTML template form cuti
2. Masukkan data sesuai dengan label
3. Print menggunakan fungsi print pada browser masing-masing pengguna

***

### 2. Catatan jatah cuti

Jumlah pengambilan cuti akan dihitung menggunakan fungsi agregat pada PostgresSQL dengan translasi query pada MqSQL seperti 

Untuk semua jenis cuti selain cuti tahunan N-1 dan cuti tahunan N-2
```sql

SELECT NIP, Tanggal, jenis_cuti, count(jenis_cuti) as jumlah FROM form_cuti
GROUP BY Tanggal
WHERE NIP = 'NIP Yang dipilih' AND YEAR(Tanggal) = 'Tahun ini'

```

Cuti tahunan N-1
```sql

SELECT NIP, Tanggal, jenis_cuti, count(jenis_cuti) as jumlah FROM form_cuti
GROUP BY Tanggal
WHERE NIP = 'NIP Yang dipilih' AND YEAR(Tanggal) = ('Tahun ini' -1) AND jenis_cuti = 'Cuti tahunan N-1'

```

Cuti tahunan N-2
```sql

SELECT NIP, Tanggal, jenis_cuti, count(jenis_cuti) as jumlah FROM form_cuti
GROUP BY Tanggal
WHERE NIP = 'NIP Yang dipilih' AND YEAR(Tanggal) = ('Tahun ini' -2) AND jenis_cuti = 'Cuti tahunan N-2'

```

Kemudian semuanya nilai akan digabungkan kedalam satu array dengan format output jenis cuti dan jumlah. 

Catatan sisa yang akan ditulis pada form akan dihitung dengan mengurangi jatah cuti dengan jumlah catatan cuti. seperti berikut

```python

catatan_cuti = [jenis_cuti, jumlah]

for index, row in enumerate(catatan_cuti):
	sisa = jatah_cuti - row[jumlah]
	catatan_cuti[index] += [sisa]

# Setelah proses loop catatan_cuti akan menjadi
# catatan_cuti = [jenis_cuti, jumlah, sisa]

```
### 3. Verifikasi dokumen/surat
Ini adalah fitur tambahan dan memang panjang kalau dikerjakan sekarang ... jadi ini tidak akan dikerjakan



## Wireframe aplikasi

### Page map
![[page-map.jpg]]

### Isi dalam halaman
1. Login
	- Form input nip dan password
	- Wallpaper
	- Logo aplikasi
2. Dashboard
	- Admin
		- Trafik form cuti dalam jangka waktu (bulan, minggu, 3 hari, dan custom)
		- Kartu informasi akun yang sedang login
		- Jumlah form cuti hari ini
		- Link list form cuti berdasarkan status
	- Atasan
		- Nama unit kerja dan logo aplikasi (kecil)
		- Trafik form cuti dalam jangka waktu (bulan, minggu, 3 hari, dan custom)
		- Kartu informasi akun yang sedang login
		- Jumlah form cuti kemarin
		- Jumlah form cuti hari ini
		- Notifikasi balasan persetujuan form cuti dari atasan
		- Link list form cuti menunggu balasan atau baru dikirim
		- Link list form cuti 
	- Pejabat
		- Nama aplikasi
		- Trafik form cuti dalam jangka waktu (bulan, minggu, 3 hari, dan custom)
		- Kartu informasi akun yang sedang login
		- Jumlah form cuti kemarin
		- Jumlah form cuti hari ini
		- Notifikasi kiriman form cuti baru
		- Link list form cuti belum dibaca
		- Link list form cuti menunggu diproses
3. Form Cuti
	- List dari semu form cuti yang ada, dengan page
	- Tombol tambah form
	- Tombol edit form
	- Tombol lihat form
	- Tombol pemberian persetujuan
4. Input form cuti
	- Form input cuti
	- Form upload file persyaratan
5. Lihat form cuti
	- Data yang telah dimasukkan
	- Preview file persyaratan
	- Status file persyaratan
6.  Ubah form cuti
	- Form edit cuti
	- Form edit file persyaratan
7. Pengaturan akun
	- Informasi akun
	- Update password
	- Delete akun
8. PNS
	- Tampilan seluruh PNS
	- Tombol lihat PNS
	- Tombol hapus PNS
9. Lihat PNS
	- Data PNS
	- Catatan cuti PNS tahun ini
	- Ubah data PNS
	- Tombol Hapus PNS
10. Ubah data PNS
	- Form edit PNS
11. Jabatan
	- Semua jabatan
12. Tampilkan jabatan
	- Deskripsi jabatan
	- Tombol hapus
	- Form ubah deskripsi
13. Unit kerja
	- Seluruh unit kerja
	- Tombol lihat
	- Tombol hapus
	- Tombol ubah unit kerja
14. Ubah unit kerja
	- Form edit deskrispi unit kerja
15. Lihat unit kerja
	- Deskrispi unit kerja
	- Atasan dan anggota badan kepegawaian
	- Tombol tambah anggota badan kepegawaian
	- Tombol hapus anggota badan kepegawaian
	- Tombol hapus atasan
	- Tombol ubah atasan
	- Tombol tambah atasan (hanya ada kalau tidak ada atasan)
16. Jenis cuti
	- Seluruh jenis cuti
	- Deskripsi jenis cuti
	- Tombol ubah deskripsi cuti
	- Tombol lihat jenis cuti
17. Lihat jenis cuti
	- Deskrispi jenis cuti
	- Persyaratan cuti
	- Jatah
18. About
	- Tentang aplikasi
	- Lisensi
	- Developer


### Template
Karena saya tidak bisa bikin layout dengan baik, maka referensi layout akan dibuat dengan menggunakan element yang sudah ada pada template. Ada 3 template yang bisa dipilih
1. [devias-io](https://github.com/devias-io)/**[material-kit-react](https://github.com/devias-io/material-kit-react)** => paling bagus
2. [Material Dahsboard](https://www.creative-tim.com/product/material-dashboard-react?partner=104080)
3. [MInimal UI](https://github.com/minimal-ui-kit/material-kit-react) 
