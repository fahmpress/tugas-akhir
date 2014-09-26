##BAB IV - PENGUJIAN EFEKTIFITAS DAN KOMPABILITAS DOCKER CONTAINER

###4.1 Pengujian Efektifitas Docker
####4.1.1 Pengujian Efektifitas Docker Dalam Penggunaan Penyimpanan (*Storage*) 
#####1. Pengujian Penggunaan Penyimpanan Pada VirtualBox

Pengujian pertama akan dilakukan pada VirtualBox. Penggunaan *storage* diukur keniakannya saja setelah proses snapshot. Buka VirtualBox dan jalankan satu mesin virtual dengan sistem operasi ubuntu.

Gambar 4.1 Sistem Operasi *guest* Ubuntu pada VirtualBox

Lihat status penggunaan *storage* sebelum melakukan snapshot dengan perintah `df`.

Gambar 4.2 Status penggunaan *storage* sebelum dilakukan snapshot

Penulis menjalankan `apt-get update` sebagai contoh untuk melakukan proses yang memperbaharui kondisi mesin virtual. Setelah itu lakukan snapshot pertama.

Gambar 4.3 Snapshot pertama

Cek status penggunaan *storage* setelah dilakukan snapshot pertama.

Gambar 4.4 Status *storage* setelah snapshot pertama

Install apache web server pada mesin virtual, lalu lakukan snapshot kedua.

Gambar 4.5 Snapshot kedua

Cek status penggunaan *storage* setelah dilakukan snapshot kedua.

Gambar 4.6 Status *storage* setelah snapshot kedua

#####2. Pengujian Penggunaan Pada Docker

Jalankan container Docker dari sistem image Ubuntu:latest. Lalu cek container yang berjalan pada terminal yg berbeda.

Gambar 4.7 Menjalankan Container Docker

Cek status penggunaan *storage* sebelum dilakukan snapshot pertama.

Gambar 4.8 Status *storage* sebelum snapshot

Lakukan proses update index *source list* pada container dengan `apt-get update` lalu ambil snapshot dengan perintah `docker commit *<container id>* *<image id>*`.

Gambar 4.9 Snapshot pertama

Cek status penggunaan *storage*.

Gambar 4.10 Status *storage* setelah snapshot pertama

Lakukan instalasi apache web server pada container, setelah itu snapshot akan diambil snapshot kedua. 

Gambar 4.11 Snapshot kedua

Lihat status penggunaan *storage* setelah pengambilan snapshot kedua.

Gambar 4.12 Status *storage* setelah snapshot kedua

Jika hasil snapshot yang disimpan dalam bentuk image dilihat secara kesuluruhan, maka akan terlihat ukuran virtual (*virtual size*) dari snapshot yang diambil lebih besar dari *base image* yang digunakan. Ini bukan ukuran image snapshot sebenarnya, namun ukuran image snapshot ditambah dengan *base image*, dimana kedua layer image tersebut akan di-*load* bersamaan ketika image snapshot dijalankan sebagai container.

Gambar 4.13 *virtual size* atau ukuran container (*base image* + image snapshot = *virtual size*)

#####3. Hasil Pengujian Efektifitas Penyimpanan

Besaran peningkatan penggunaan *storage* akan dihitung dengan cara mengurangi status penggunaan *storage* setelah snapshot terakhir, dikurangi status penggunaan *storage* sebelum dilakukan snapshot. Pengukuran dilakukan pada partisi `/root`, karena penulis hanya menggunakan satu partisi pada mesin host untuk mendapatkan akurasi dalam pengukuran.

Penggunaan *storage* pada VirtualBox adalah sebagai berikut:

7496284-6778920= 717364 bytes

Sedangkan penggunaan *storage* pada docker adalah:

7594024-7497764= 96260 bytes 

####4.1.2 Pengujian Efektifitas Docker Dalam Penggunaan Memory
...

###4.2 Pengujian Kompabilitas Docker 
####4.2.1 Pengujian Kompabilitas Docker Terhadap Perbedaanan Platform
...

####4.2.2 Pengujian Kompabilitas Docker Terhadap Perbedaan *Environment* Host
...

####4.2.3 Pengujian Kompabilitas Docker Terhadap Perbedaan Versi Aplikasi 
...