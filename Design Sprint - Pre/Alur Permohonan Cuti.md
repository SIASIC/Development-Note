[[Design Sprint - Pre]]

## General
1. PNS bertemu dengan atasan unit kerja untuk mengajukan cuti dan menyerahkan [[Persyaratan Cuti]]
2. Atasan mengisikan [[Form Cuti]] dan memasukkan [[Persyaratan Cuti]] yang diberikan oleh pegawai
3. Form cuti yang telah disetujui diteruskan kepada pejabat yang bersangkutan

[[Atasan dan pejabat yang bersangkutan]] 

#### Status form cuti
Form cuti bisa disetujui oleh Atasan dan Pejabat yang bersangkutan. Atasan dan Pejabat bisa memberikan status pada form cuti berupa
1. Disetujui
2. Perubahan
3. Ditangguhkan
4. Tidak disetujui

Status dari atasan menetapkan bahwa form cuti
- Jika disetujui maka form cuti akan diteruskan kepada pejabata yang berwenang
- Jika perubahan maka form cuti akan diberikan kembali ke pemohon dengan alasan apa yang harus diubah
- Jika Ditangguhkan maka form cuti akan sementara ditahan dan menunggu proses lebih lanjut
- Jika Tidak disetujui maka form cuti akan diberikan kembali pemohon

Status dari pejabat menetapkan bahwa form cuti
- Jika disetujui maka form cuti akan disetuji dan pemohon bisa melakukan cuti
- Jika perubahan maka form cuti akan diberikan kembali ke atasan yang bersangkutan dengan alasan apa yang harus diubah
- Jika Ditangguhkan maka form cuti akan sementara ditahan dan menunggu proses lebih lanjut
- Jika Tidak disetujui maka form cuti akan diberikan kembali ke atasan yang bersangkutan

## Refine
1. Atasan mengisi data diri (otomatis diisi)
2. Atasan memilih jenis cuti yang diambil
3. Atasan mengisi alasan cuti
4. Mengisi
	- Lama cuti hari/bulan/tahun
	- Mulai tanggal (akan diisi otomatis hari ini, tapi bisa diubah)
	- Sampai dengan (akan diisi otomatis oleh mesin, supaya tidak terjadi kesalahan)
	Sampai dengan  = mulai tanggal + lama cuti (hari)
5. Mesin akan mengambil catatan cuti berupa
	- Jumlah cuti tahunan yang diambil selama kurun 3 tahun
	- Jumlah cuti lainnya yang diambil selama tahun ini

#### format pengambilan catatan cuti: 
| Jenis Cuti                     | Jumlah | Sisa |
|--------------------------------|---------|------|
| Cuti tahunan N-2               |         |      |
| Cuti tahunan N-1               |         |      |
| Cuti tahunan N                 |         |      |
| Cuti Besar                     |         |      |
| Cuti Melahirkan                |         |      |
| Cuti Karena alasan penting     |         |      |
| Cuti di luar tanggungan negara |         |      |

6. Atasan mengisi alamat selama menjalankan cuti
7. Atasan mengisi no telp yang bisa dihubungi selama menjalan cuti
8. Memasukkan persyaratan cuti sesuai dengan [[Persyaratan Cuti]]
9. Atasan mempertimbangkan form cuti [[Alur Permohonan Cuti#Status form cuti]]
10. Pejabat mempertimbangkan form cuti [[Alur Permohonan Cuti#Status form cuti]]
