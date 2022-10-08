[[Design Sprint - Pre]]

## Referensi Jurnal



## Langkah verifikasi (roughly)
1. Identifikasi sesuai dengan [[Persyaratan Cuti#Kriteria persyaratan cuti]]
2. Keluarkan output "Terverifikasi" atau "Tidak Terverifikasi"
3. Langkah selanjutnya sesuai dengan verifikasi masing-masing dokumen

## Verifikasi surat dokter dan surat bidan
1. Segmentasi surat menjadi 3 bagian
	- Kop surat
	- Isi
	- Penutup atau bagian tanda tangan
2. Identifikasi dari 3 bagian
	- Kop surat mirip dengan milik ketentuan keluaran dari dinas
	- Nama dari dokter/bidan yang bersangkutan ada dalam database sebagai dokter/bidan
	- Tanda tangan benar milik dokter/bidan yang bersangkutan
	Setiap bagian memiliki outpout 0 atau 1
3. Syarat outpout "Terverifikasi" adalah dengan output identifikasi Kop surat dan nama dokter/bidan adalah 1, selain itu output akan menjadi "Tidak terverifikasi"
4. Atasan atau Badan kepegawaian bisa merubah status surat dari "Tidak Terverifikasi" menjadi "Terverifikasi" dan membuat mesin melakukan
	- Menambah nilai fitur kop surat kedalam data training dan membuat model baru berdasarkan kop surat yang berada dalam surat, jika kop surat memiliki nilai identifikasi 0
	- Menambahkan nama dokter/bidan kedalam database, jika nama dokter/bidan memiliki nilai identifikasi 0
	- Menambah nilai fitur tanda tangan kedalam data training dan membuat model baru berdasarkan tanda tangan yang berada dalam surat, jika tanda tangan memiliki nilai identifikasi 0
