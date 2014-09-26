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
#####1 Membangun Aplikasi PHP Pada Sistem Operasi Ubuntu 14.04 LTS

Pada pengujian ini penulis menggunakan Dockerfile dari tutum/lamp repository untuk membangun sebuah aplikasi web, lalu menggunakan aplikasi PHP degan *source code* yang telah penulis siapkan pada Github. Aplikasi PHP ini dibangun pada komputer dengan sistem operasi Ubuntu 14.04 LTS dan akan dijalankan pada sistem operasi CentOS 6.5.
Berikut kode Dockerfile tutum/lamp:

    FROM ubuntu:trusty
    MAINTAINER Fernando Mayo <fernando@tutum.co>, Feng Honglin  <hfeng@tutum.co>

    # Install packages
    RUN apt-get update 
    RUN DEBIAN_FRONTEND=noninteractive apt-get -y install supervisor 
    RUN DEBIAN_FRONTEND=noninteractive apt-get -y install git 
    RUN DEBIAN_FRONTEND=noninteractive apt-get -y install apache2 
    RUN DEBIAN_FRONTEND=noninteractive apt-get -y install libapache2-mod-php5
    RUN DEBIAN_FRONTEND=noninteractive apt-get -y install mysql-server 
    RUN DEBIAN_FRONTEND=noninteractive apt-get -y install php5-mysql 
    RUN DEBIAN_FRONTEND=noninteractive apt-get -y install pwgen 
    RUN DEBIAN_FRONTEND=noninteractive apt-get -y install php-apc

    # Add image configuration and scripts
    ADD start-apache2.sh /start-apache2.sh
    ADD start-mysqld.sh /start-mysqld.sh
    ADD run.sh /run.sh
    RUN chmod 755 /*.sh
    ADD my.cnf /etc/mysql/conf.d/my.cnf
    ADD supervisord-apache2.conf /etc/supervisor/conf.d/supervisord-        apache2.conf
    ADD supervisord-mysqld.conf /etc/supervisor/conf.d/supervisord- mysqld.conf

    # Remove pre-installed database
    RUN rm -rf /var/lib/mysql/*

    # Add MySQL utils
    ADD create_mysql_admin_user.sh /create_mysql_admin_user.sh
    RUN chmod 755 /*.sh
    
    # config to enable .htaccess
    ADD apache_default /etc/apache2/sites-available/000-default.conf
    RUN a2enmod rewrite
    
    # Configure /app folder with sample app
    RUN git clone https://github.com/fermayo/hello-world-lamp.git /app
    RUN mkdir -p /app && rm -fr /var/www/html && ln -s /app     /var/www/html
    
    #Enviornment variables to configure php
    ENV PHP_UPLOAD_MAX_FILESIZE 10M
    ENV PHP_POST_MAX_SIZE 10M

    # Add volumes for MySQL 
    VOLUME  ["/etc/mysql", "/var/lib/mysql" ]
    
    EXPOSE 80 3306
    CMD ["/run.sh"]
    
Simpan kode tersebut dengan nama Dockerfile, lalu eksekusi dengan perintah `docker build -t <username/nama> .` dimana Dockerfile berada.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.20.png "Gambar 4.20")

Gambar 4.20 Proses Dockerfile tutum/lamp dalam membangun aplikasi web

Dockerfile tersebut akan membuat sebuah LAMP server berikut aplikasi PHP di dalamnya. Aplikasi PHP tersebut akan diganti menggunakan aplikasi yang sudah disiapkan penulis.

Buat Dockerfile pada folder yang berbeda, dengan kode sebagai berikut:

    FROM tutum/lamp:latest
    RUN rm -fr /app && git clone https://github.com/fahmpress/mycustomapp1.git  /app
    EXPOSE 80 3306
    CMD ["/run.sh"]

Setelah itu jalankan Dockerfile.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.21.png "Gambar 4.21")

Gambar 4.21 Proses Dockerfile untuk kostumasi aplikasi PHP

Jalankan container LAMP Server tersebut dengan perintah:

    # docker run -d -p 80:80 -p 3306:3306 username/nama-aplikasi

Akses web server yang sudah dibuat melalui mesin host.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.22.png "Gambar 4.22")

Gambar 4.22 LAMP Server dengan kustomasi aplikasi PHP

Aplikasi PHP yang dipaketkan dengan LAMP server berhasil dibuat. Selanjutnya aplikasi akan dijalankan di sistem operasi Centos untuk menguji container Docker yang dibuat kompatible pada sistem operasi yang berbeda.

#####2 Menjalankan Aplikasi PHP Pada Sistem Operasi CentOS 6.5

Simpan image aplikasi PHP yang telah dibuat ke dalam format .tar dengan perintah:

    #  docker save fahmpress/mylamp > /home/fahm/mylamp.tar

lalu pindahkan melalui SFTP server ke mesin CentOS 6.5

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.23.png "Gambar 4.23")

Gambar 4.23 Memindahkan file image melalui SFTP server

Load image dalam format .tar tersebut setelah itu cek apakah sudah tersedia pada mesin host, lalu jalankan image tersebut.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.24.png "Gambar 4.24")

Gambar 4.24 Me-*load* dan menjalankan image pada OS CentOS 6.5

Setelah itu akses lamp server melalui browser.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar4.25.png "Gambar 4.25")

Gambar 4.25 LAMP server berhasil dijalan pada OS CentOS

####4.2.2 Pengujian Kompabilitas Docker Terhadap Perbedaan *Environment* Host


####4.2.3 Pengujian Kompabilitas Docker Terhadap Perbedaan Versi Aplikasi 
...