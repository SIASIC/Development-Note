[[Design Sprint - Pre]]

[[Persyaratan Cuti]]

## Otomatis berada pada surat
1. Kepada
2. Tempat, tanggal

## Form yang harus diisi pemohon
### Data pegawai
1. Nama
2. Jabatan
3. Unit kerja
4. NIP
5. Masa kerja

> Bisa diisi otomatis oleh mesin menggunakan NIP atau isi otomatis di aplikasi pemohon izin

### Jenis Cuti
Memilih jenis cuti
1. Cuti tahunan
2. Cuti besar
3. Cuti Sakit
4. Cuti Melahirkan
5. Cuti Karena alasan penting
6. Cuti diluar tanggungan negara

### Alasan cuti
Alasan kenapa cuti berbentuk text

### Lama cuti
1. Selama. Lama menggunakan angka dengan pilihan hari, bulan, dan tahun. Simpan data sebagai hari dikali kelipatan hari, bulan, atau tahun.
2. Mulai tanggal. **
3. sampai dengan. **

> ** Bisa diisi manual, tapi akan diisi otomatis oleh mesin.
> Error akan muncul jika selisih mulai tanggal dan sampai dengan kurang dari selama
> Perbaikan bisa dilakukan otomatis. Bisa memilih untuk memperbaiki selama atau memperbaiki mulai tanggal atau sampai tanggal

> Mulai tanggal akan otomatis set tanggal hari ini
> Sampai dengan akan diisi otomatis setelah memilih Mulai tanggal dengan nilai Selama ditambah nilai Mulai tanggal

### Catatan Cuti
Jumlah setiap cuti yang telah diambil

> Diisi otomatis oleh mesin

### Alamat selama cuti
1. Alamat lengkap
2. Nomor telepon  yang bisa dihubungi
3. Tanda tangan
4. NIP (diisi otomatis)

* * * 

## Proses persetujuan

> Bagian ini diisi oleh atasan dan pejabat yang bersangkutan

[[Atasan dan pejabat yang bersangkutan]]

### Pertimbangan atasan langsung
atasan memilih status dari surat
1. Disetujui
2. Perubahan
3. Ditangguhkan
4. Tidak disetujui

Ditambah dengan
1. Tanda tangan
2. NIP
Otomatis diisi oleh mesin ketika disetujui


### Keputusan pejabat berwenang yang memberikan cuti
atasan memilih status dari surat
1. Disetujui
2. Perubahan
3. Ditangguhkan
4. Tidak disetujui

Ditambah dengan
1. Tanda tangan
2. NIP
Otomatis diisi oleh mesin ketika disetujui

