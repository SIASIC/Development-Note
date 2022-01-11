#design-sprint 

Yang harus dilakukan hari ini
- [x] Memecah solusi atau masalah menjadi beberapa bagian kecil
- [ ] Membuat wireframe aplikasi

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

**Lanjut pikirkan nanti**

***

### 2. Catatan jatah cuti

Jumlah pengambilan cuti akan dihitung menggunakan fungsi agregat pada mongodb dengan translasi query pada MqSQL seperti 

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