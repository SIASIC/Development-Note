[[Design Sprint]]

### Yang harus dilakukan
- [x] Menentukan solusi yang akan digunakan
- [x] Menemukan seluruh masalah yang bisa terjadi pada solusi
- [x] Menentukan resource yang diperlukan

![[Pasted image 20220112082124.png]]

## Solusi yang digunakan
1. Entry data otomatis akan dilakukan dengan mengambil dari data dari API [[2022-01-12]], sedangkan data yang lain akan dimasukkan secara manual. Data dari API akan tetap disimpan dan tidak akan menggunakan data referensi, karena form cuti akan menjadi track record selamanya dan tidak akan hilang.
2. Print form cuti dilakukan dengan menggunakan halaman HTML sebagai perantara print dengan membuat template form cuti dari HTML, kemudian mengisi label dengan data yang telah dimasukkan. Pembuatan HTML akan digunakan menggunakan fungsi save as .html dari ms office word. 
3. Catatan jatah cuti akan diambil dari database dan dihitung menggunakan query [[2 - Sketch#2 Catatan jatah cuti]]
4. Verifikasi dokumen dan surat akan dikembangkan setelah fitur utama selesai.

## Masalah yang mungkin terjadi
1. Pengambilan API kemungkinan harus dilakukan dengan mengakses OTP / TOTP, jadi harus minta kunci dan membuat program untuk verifikasi.
2. File HTML mungkina akan sedikit tidak mirip, khsusunya di pembagian halaman
3. Catatan jumlah cuti akan sangat berat jika dihitung tiap ditampilkan pada halaman lihat PNS, harus melihat bagaimana sistem updating cache di django.
4. Verifikasi dokumen dan surat harus dibuat seperti module tambahan dan bisa ditambahkan pada sistem, tanpa merusak atau mengubah terlalu banyak sistem yang telah dibuat.

## Resource
### Teknologi yang digunakan
1. JavaScript -> bahasa pemrograman untuk front end aplikasi
2. ReactJS -> Framework front end aplikasi
3. Python -> bahasa pemrograman untuk back end aplikasi dan juga bahasa pemrograman yang akan digunakan untuk AI dan Computer Vision pada dokumen [[Persyaratan Cuti]]
4. Django -> Framework back end aplikasi
5. PostgresSQL -> karena memakai Django

### Users
User tetap dibagi menjadi 3, yaitu
1. Admin -> Akun yang memiliki semua hak akses dari semua data yang ada
2. Atasan / Bagian Kepegawaian -> Akun yang bertugas untuk membantu pengisian form milik PNS dan melakukan persetujuan form cuti pada Unit kerja masing-masing sebelum form cuti dikirim ke pejabat bersangkutan
3. Pejabat -> Akun yang menerima form cuti berstempel dan memberikan persetujuan akhir

### Budget
(kalau ada)

1. Hosting Django dan PostgresSQL -> Jika ingin performa yang bagus $75 perbulan, jika dirasa tidak perlu maka bisa gratis
2. Admin template berbayar -> $69 up


