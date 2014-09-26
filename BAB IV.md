##BAB IV - PENGUJIAN EFEKTIFITAS DAN KOMPABILITAS DOCKER CONTAINER

###4.1 Pengujian Efektifitas Docker
####4.1.1 Pengujian Efektifitas Docker Dalam Penggunaan Penyimpanan (*Storage*) 
#####1. Pengujian Penggunaan Penyimpanan Pada VirtualBox

Pengujian pertama akan dilakukan pada VirtualBox. Penggunaan *storage* diukur keniakannya saja setelah proses snapshot. Buka VirtualBox dan jalankan satu mesin virtual dengan sistem operasi ubuntu.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.1.png "Gambar 4.1")

Gambar 4.1 Sistem Operasi *guest* Ubuntu pada VirtualBox

Lihat status penggunaan *storage* sebelum melakukan snapshot dengan perintah `df`.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.2.png "Gambar 4.2")

Gambar 4.2 Status penggunaan *storage* sebelum dilakukan snapshot

Penulis menjalankan `apt-get update` sebagai contoh untuk melakukan proses yang memperbaharui kondisi mesin virtual. Setelah itu lakukan snapshot pertama.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.3.png "Gambar 4.3")

Gambar 4.3 Snapshot pertama

Cek status penggunaan *storage* setelah dilakukan snapshot pertama.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.4.png "Gambar 4.4")

Gambar 4.4 Status *storage* setelah snapshot pertama

Install apache web server pada mesin virtual, lalu lakukan snapshot kedua.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.5.png "Gambar 4.5")

Gambar 4.5 Snapshot kedua

Cek status penggunaan *storage* setelah dilakukan snapshot kedua.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.6.png "Gambar 4.6")

Gambar 4.6 Status *storage* setelah snapshot kedua

#####2. Pengujian Penggunaan Penyimpanan Pada Docker

Jalankan container Docker dari sistem image Ubuntu:latest. Lalu cek container yang berjalan pada terminal yg berbeda.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.7.png "Gambar 4.7")

Gambar 4.7 Menjalankan Container Docker

Cek status penggunaan *storage* sebelum dilakukan snapshot pertama.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.8.png "Gambar 4.8")

Gambar 4.8 Status *storage* sebelum snapshot

Lakukan proses update index *source list* pada container dengan `apt-get update` lalu ambil snapshot dengan perintah `docker commit *<container id>* *<image id>*`.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.9.png "Gambar 4.9")

Gambar 4.9 Snapshot pertama

Cek status penggunaan *storage*.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.10.png "Gambar 4.10")

Gambar 4.10 Status *storage* setelah snapshot pertama

Lakukan instalasi apache web server pada container, setelah itu snapshot akan diambil snapshot kedua. 

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.11.png "Gambar 4.11")

Gambar 4.11 Snapshot kedua

Lihat status penggunaan *storage* setelah pengambilan snapshot kedua.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.12.png "Gambar 4.12")

Gambar 4.12 Status *storage* setelah snapshot kedua

Jika hasil snapshot yang disimpan dalam bentuk image dilihat secara kesuluruhan, maka akan terlihat ukuran virtual (*virtual size*) dari snapshot yang diambil lebih besar dari *base image* yang digunakan. Ini bukan ukuran image snapshot sebenarnya, namun ukuran image snapshot ditambah dengan *base image*, dimana kedua layer image tersebut akan di-*load* bersamaan ketika image snapshot dijalankan sebagai container.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.13.png "Gambar 4.13")

Gambar 4.13 *virtual size* atau ukuran container (*base image* + image snapshot = *virtual size*)

#####3. Hasil Pengujian Efektifitas Penyimpanan

Hasil pengujian penggunaan *storage* akan dihitung dengan cara mengurangi status penggunaan *storage* setelah snapshot terakhir, dikurangi status penggunaan *storage* sebelum dilakukan snapshot. Pengukuran dilakukan pada partisi `/root`, karena penulis hanya menggunakan satu partisi pada mesin host untuk mendapatkan akurasi dalam pengukuran.

Penggunaan *storage* pada VirtualBox adalah sebagai berikut:

7496284-6778920= 717364 bytes

Sedangkan penggunaan *storage* pada docker adalah:

7594024-7497764= 96260 bytes 

####4.1.2 Pengujian Efektifitas Docker Dalam Penggunaan Memory
#####1 Pengujian Penggunaan Memory Virtual Mesin Pada VirtualBox

Pada pengujian ini penulis menjalankan 5 mesin virtual pada VirtualBox hasil duplikat dengan metode duplikasi *linked clone* dengan besar memory yang dipakai 192 MB. Pertama cek kapasitas penggunaan memory dengan perintah `top` sebelum mesin virtual di jalankan.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.14.png "Gambar 4.14")

Gambar 4.14 Status penggunaan memory sebelum menjalankan mesin virtual

Jalankan 5 mesin virtual pada VirtualBox.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.15.png "Gambar 4.15")

Gambar 4.15 Menjalankan 5 mesin virtual pada VirtualBox

Cek kapasistas penggunaan dan peningkatan memory setelah mesin virtual diajalankan.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.16.png "Gambar 4.16")

Gambar 4.16 Status memory setelah menjalankan mesin virtual

#####2 Pengujian Penggunaan Memory Conatainer Docker

Untuk melakukan pengujian pada container, penulis menjalankan container lebih banyak dari virtual mesin, yaitu 10 Container. Cek penggunaan memory sebelum menjalankan container.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.17.png "Gambar 4.17")

Gambar 4.17 Status penggunaan memory sebelum menjalankan container

Jalankan 10 container `Ubuntu:latest` dengan perintah `docker run -i -t -d ubuntu /bin/bash`, perintah ini memerintahkan docker untuk menjalankan container pada mode *background*.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.18.png "Gambar 4.18")

Gambar 4.18 Menjalankan 10 container Docker

Cek status penggunaan memory setelah menjalankan container.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.19.png "Gambar 4.19")

Gambar 4.19 status penggunaan memory setelah menjalankan 10 container

#####3 Hasil Pengujian Penggunaan Memory

Hasil pengujian penggunaan memory akan dihitung dengan mengurangi besaran penggunaan memory setelah menjalankan mesin virtual dengan besaran penggunaan memory sebelum menjalan mesin virtual. VirtualBox menjalankan 5 mesin virtual dengan penggunaan memory sebesar:

2193672-1006232= 1187440 bytes

sedangkan penggunaan memory 10 container Docker adalah:

1093896-1066364= 27532 bytes

###4.2 Pengujian Kompabilitas Docker 
####4.2.1 Pengujian Kompabilitas Docker Terhadap Perbedaanan Platform
...

####4.2.2 Pengujian Kompabilitas Docker Terhadap Perbedaan *Environment* Host
...

####4.2.3 Pengujian Kompabilitas Docker Terhadap Perbedaan Versi Aplikasi 
...