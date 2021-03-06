##BAB III -  PERANCANGAN DAN IMPLEMENTASI


###3.1	Skenario Pengujian

Pengujian dilakukan untuk menguji keunggulan Dokcer dalam hal proses *deployment* yang dianggap bisa mengatasi kekurangan pada virtualisasi sebelumnya menggunakan mesin virtual tradisional. Selain itu, pengujian dilakukan juga untuk menjawab permasalahan yang sering terjadi dalam pengembangan aplikasi web. Untuk menjawab hal tersebut, dalam penulisan ini akan dibahas mengenai skenerio dan metode pengujiannya. 

####3.1.1	Uji Efektifitas Docker Dalam Penggunaan Sumber Daya
Docker merupakan Platform as a Service yang menggunakan teknologi virtualisasi yang lebih maju dari virtualisasi sebelumnya, sehingga virtualisasi sebelumnya disebut sebagai virtualisasi tradisional. Untuk itu, teknologi virtualisasi ini dijadikan sebagai bahan analisa untuk membandingkan kinerja teknologi virtualisasi Docker dengan virtualisasi tradisional. Ada dua parameter yang akan digunakan sebagai variasi uji dalam pengehematan sumber daya, yaitu penghematan penyimpanan dan memory.

#####3.1.1.1	Penghematan Penyimpanan (*Storage*)
1. Union File System

Dalam Linux boot tradisional, kernel pertama kali menggunakan (*mount*) *root file system* sebagai *read-only*, memeriksa integritasnya, lalu mengganti keseluruhan `rootfs` menjadi mode *read-write*.

Sama seperti Linux boot tradisional, `rootfs` pada Docker akan di-*mount* pertama kali dalam mode *read-only*, namun kemudian, tidak merubah file system menjadi mode *read-write*, Docker mengambil keuntungan dari *union mount* untuk menambah file system *read-write* di atas file system read-only*. Hasilnya, akan ada beberapa file system *read-only* ditumpuk di atasnya satu sama lain. 

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.1.jpg "Gambar 3.1")

Gambar 3.1 File system as a Layer

Pertama kali, tidak ada apa-apa pada lapisan *read-write* paling atas, namun kapan saja berjalan sebuah proses akan menghasilkan sebuah file, hal ini terjadi pada lapisan di atasnya. Dan jika sesuatu memerlukan *update* pada file yang berada di lapisan lebih rendah, maka file akan disalin ke lapisan yang lebih atas dan perubahan berbentuk sebuah salinan. Versi file di lapisan di bawahnya tidak bisa lagi terlihat oleh aplikasi, padahal sebenarnya ada, dan tidak berubah.

Mekanisme file system yang menjadi *back-end* container Docker ini disebut **Union File System**. Hal inilah yang menjadikan proses *deployment* container Docker menjadi efektif dalam hal penyimpanan dibanding dengan mesin virtual tradisional seperti VirtualBox, Docker tidak akan membuat snapshot dengan menyalin seluruh file sistem yang ada sebagai image, namun hanya menyalin lapisan perubahannya saja.

2. Metode Uji dengan Studi Komparasi

Sesuai paparan di atas terlihat perbedaan penggunaan penyimpanan Docker dengan mesin virtual tradisional. Dalam hal ini penulis akan melakukan pembuktian terhadap teori tersebut dengan melakukan komparasi antara Docker dan VirtualBox, sehingga terlihat efektifitas Docker dibandingkan mesin virtual tradisional.

Untuk malakukan pengujian tersebut penulis akan menginstall Docker dan VirtualBox pada mesin host dan sistem operasi yang sama secara bergantian agar hardware yang digunakan identik dan sama persis, hal ini dilakukan atas pertimbangan integritas pengujian. Lalu menjalankan satu mesin virtual (container) dan melakukan 2 proses yang masing-masing proses akan diambil snapshot-nya. Pengukuran penggunaan *storage* diambil sebelum melakukan snapshot dan setelah pengambilan snapshot, lalu dibandingkan berapa peningkatan *storage* yang digunakan antara virtualbox dan Docker. Proses ini dilakukan bergantian antara Virtualbox dan Docker. Parameter uji yang digunakan dalam pengujian ini adalah besaran penggunaan penyimpanan (*storage*).

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.2.png "Gambar 3.2")

Gambar 3.2 Metode Pengujian

#####3.1.1.2.	Penghematan Memory
Dalam proses deployment-nya Docker container menggunakan shared kernel dari mesin host tanpa ada perantara lapisan virtualisasi seperti *hypervisor*, maka proses menjadi lebih ringan sehingga bisa menghemat memory dan overhead pada mesin host (*zero overhead*) sehingga memungkinkan untuk menjalankan banyak container dalam satu mesin, berbeda dengan virtualisasi tradisional yang menggunakan *hypervisor* dan kernel tersendiri dari mesin host.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.3.jpg "Gambar 3.3")

Gambar 3.2 Shared Host Kernel pada Docker

Untuk pengujian ini akan dilakukan komparasi saat proses *deployment* mesin virtual (container) antara Docker dan VirtualBox. Docker dan Virtualbox akan diinstal pada mesin host dan sistem operasi yang sama. Setelah itu akan dijalankan beberapa mesin virtual dan container lalu akan dilihat penggunaan memorynya. Pengukuran memory akan menggunakan top, yang secara *default* sudah tersedia pada OS Ubuntu 14.04. Parameter uji dalam pengujian ini adalah besaran kenaikan memory yang digunakan saat menjalankan mesin virtual atau container.

####3.1.2	Uji Kompabilitas Docker

Aplikasi yang sudah diinstall, dipaketkan dan dijalankan menggunakan container Docker disebut *Dockerized app*, Docker mengklaim sekali *developer* software membangun aplikasi dengan container, maka *dockerized app* bisa dijalankan di hampir semua *environment* seperti virtual mesin, Laptop, cloud, bare metal, dan lain-lain. Dalam hal ini penulis akan menguji hal tersebut dengan menjalankan *dockerized app* pada *environment* yang berbeda termasuk kompabilitas dengan lingkungan host yang mempunyai masalah *conflicting dependencies*.

#####3.1.2.1	Uji Kompabilitas Container Docker Terhadap Perbedaan Platform

1. *Cross-platform Dependencies*

Idealnya, developer aplikasi harus mampu membuat aplikasi yang fleksibel yang mampu dijalankan lintas platform untuk dapat menangani kasus seperti migrasi server ke server lain dengan sistem operasi yang berbeda. Namun pada kenyataannya hal ini sulit untuk diimplementasikan karena ketergantungan aplikasi terhadap suatu platform atau permasalahan yang biasa disebut *cross-platform dependencies*, dimana *sysadmin* harus mengkonfigurasi ulang *environment* baru untuk aplikasinya karena perbedaan sistem operasi server dan versi kernel.

Docker menjawab permasalahan tersebut dengan containernya. Aplikasi yang sudah di-*package* menjadi *dockerized app* bersama semua *dependencies*-nya menggunakan container akan mampu berjalan pada platform yang menjalankan Docker (*enable dokcer engine*) tanpa harus merubah dan mengkonfigurasi apapun pada container ataupun mesin host.

2.	Metode Pengujian

Pengujian akan dilakukan dengan metode simulasi (virtual mesin sebagai mesin host untuk Docker) dengan menginstall Web server pada 2 mesin virtual yang masing-masing menggunakan sistem operasi Linux yang berbeda distro (Ubuntu 14.04 dan CentOS 7). Web server akan diinstall dengan menggunakan container pada mesin Ubuntu, lalu *dockerized* web server tersebut akan dijalankan di mesin CentOS tanpa melakukan perubahan apapun pada mesin host ataupun container.

#####3.1.2.2 Uji Kompabilitas Container Docker Terhadap Perbedaan *Environment* Host

1.	Pentingnya Fleksibilitas Aplikasi

Contoh kasus, dalam pengembangan aplikasi dengan skala *enterprise* seperti pada perusahaan bisnis, aplikasi yang dikembangkan sebagai servis yang dijalankan untuk *customers* harus memenuhi standar mutu dan spesifikasi yang dibutuhkan perusahaan. Untuk itu aplikasi yang telah dibangun oleh *developer* pada mesin lokalnya (semisal Laptop) akan diuji kelayakannya pada hardware Quality Assurance (QA Server). QA Server akan melakukan validitas untuk memastikan aplikasi tersebut memenuhi spesifikasi QC (*Quality Control*) dan menguji fitur serta fungsionalitasnya agar sesuai dengan sasaran pelaku bisnis. Setelah itu aplikasi akan dijalankan (di-*hosting*) pada hardware yang berbeda pula, misalnya Cloud (*Private/Public*), bare metal, virtual server, virtual mesin, dan sebagainya.

Pada kasus diatas, aplikasi harus mempunyai fleksibilitas tinggi agar mampu dijalankan pada hardware yang berbeda, hal ini dimaksudkan untuk menghindari kesalahan atau error saat melakukan re-*packaging dependencies* dan konfigurasi yang dibutuhkan oleh aplikasi tersebut. Dengan Docker hal itu tidak akan menjadi permasalahan yang berarti selama hardware support untuk menjalankan Docker engine. Docker memastikan lingkungan host tidak akan berpengaruh pada container dan lingkungan container akan sama persis seperti saat dimana dia dibuat. Oleh karena itu *Dockerized app* yang sudah dibangun akan mampu dijalankan dimanapun yang menjalankan Docker engine tanpa harus melakukan perubahan apapun.

2.	Metode Pengujian

Perbedaan *environment* host yang dimaksudkan penulis meliputi; perbedaan pada layer hardware (virtual/fisik), konfigurasi sistem (Normal server/QA Server), lingkungan hosting (*Cloud*/lokal), dan lain-lain. Pengujian akan dilakukan dengan menjalankan *dockerized app* pada lingkungan host yang berbeda sesuai dengan kriteria di atas. Untuk membuktikan bahwa *dockerized app* bisa dijalankan pada host yang jenisnya berbeda.

Penulis akan membangun *Dockerized app* pada virtual mesin yang menggunakan hypervisor tipe2, lalu aplikasi tersebut akan dijalankan pada hardware Laptop. Hal ini termasuk pada kriteria *environment* yang berbeda seperti disebutkan di atas, karena virtual mesin yang menggunakan metode virtualisasi penuh dengan teknologi hypervisor type 2 bersifat independent dan terpisah dari mesin host. Pada realitasnya hal ini bisa terjadi pada saat aplikasi dijalankan oleh perusahaan yang melakukan konsolidasi server dengan virtualisasi seperti VirtualBox dan VMWare.

#####3.1.2.3 Uji Kompabilitas Container Docker Terhadap Perbedaan Versi Aplikasi

1.	*Conflicting Dependencies*

Beberapa aplikasi berbeda yang berjalan pada host yang sama kadang kali mendapat masalah ketika tergantung pada library yang sama namun versinya berbeda. Hal ini menjadikan aplikasi tidak bisa berjalan bersama-sama. Atau masalah pada perbedaan versi aplikasi itu sendiri. Penulis mengambil contoh kasus pengembangan web PHP, ketika sebuah perusahaan memiliki aplikasi pada *server farm*-nya dengan kode yang ditulis menggunakan PHP3 atau PHP4, lalu membuat aplikasi baru menggunakan PHP5 dengan alasan penggunaan fitur yang tidak terdapat pada versi sebelumnya. Solusinya adalah menjalankan server PHP pada mesin yang berbeda, atau melakukan upgrade pada kode programnya. Namun opsi pertama tidak bisa dilakukan jika perusahaan tidak ingin server PHP dijalankan pada mesin yang terpisah untuk alasan keamanan. Hal ini tentu saja menjadi masalah yang berhubungan dengan biaya dan waktu yang dapat merugikan perusahaan. 

Dengan Docker, dapat dipastikan tidak terjadi konflik untuk menjalankan aplikasi yang berbeda versi untuk menjawab permasalahan diatas. Container Docker menjamin bahwa aplikasi yang berjalan di dalamnya diisolasi tanpa mempengaruhi lingkungan host juga container lain dan *zero overhead*, yang brarti terdapat keuntungan juga pada penggunaan sumber daya dibandingkan harus melakukan konsolidasi server menggunakan virtual mesin. 

2.	Metode Pengujian

Untuk metode pengujian penulis akan menjalankan aplikasi web PHP yang berbeda versi (PHP4 dan PHP5) pada mesin host yang sama.

###3.2	Pemilihan Software dan Sistem Operasi

Sesuai skenerio dan metode yang dipaparkan di atas, jumlah variasi pengujian adalah 5 variasi uji. Untuk melakukan pengujian tersebut penulis menggunakan software dan sistem operasi Linux dengan distribusi yang berbeda.

####3.2.1	Pemilihan Software

Software yang digunakan dalam pengujian ini terdiri dari software yang digunakan sebagai; aplikasi contoh, software virtualisasi untuk uji komparasi, dan *tool* untuk pengukuran sumber daya.

1.	Apache & PHP

Apache adalah sebuah software HTTP server yang memainkan peran penting dalam perkembangan web (WWW), sedangkan PHP merupakan bahasa pemerograman *server-side* untuk aplikasi web itu sendiri. Kedua software untuk membangun sebuah web server ini sangat familiar dikalangan *developer* aplikasi berbasis web. Untuk itulah penulis memilih Apache dan PHP sebagai media uji pada pengujian ini. 

Apache dan PHP ini akan digunakan untuk 3 variasi uji pada point uji kompabilitas container Docker. Versi PHP yang digunakan adalah PHP4 dan PHP5.   

2.	VMware Workstation

VMware Workstation adalah hypervisor yang berjalan di komputer x64. Memungkinkan pengguna untuk membuat mesin virtual dalam satu mesin fisik. MVware workstation merupakan softwre virtualisasi dengan hypervisor tipe 2. Dalam karya tulis ini VMware Workstation akan digunakan sebagai alat pengujian pada variasi uji uji kompabilitas terhadap perbadaan lingkungan host. 

3.	VirtualBox

Oracle VM VirtualBox merupakan paket software virtualisasi untuk komputer x86 dan AMD64/Intel64 dari Oracle Corporation sebagai bagian keluarga dari produk virtualisasi. VirtualBox sama seperti VMware, merupakan virtualisasi dengan menggunakan hypervisor tipe 2 yang menjalankan lapisan virtualisasi di atas komputer host. Pada pengujian ini VirtualBox akan digunakan sebagai alat komparasi dengan Docker pada pengujian pengehematan sumber daya.

####3.2.2	Pemilihan Sistem Operasi

Docker hanya bisa berjalan pada kernel yang sudah ditentukan yaitu 3.8 ke atas, namun sistem operasi yang memiliki kernel dibawahnya tetap bisa menjalankan Docker dengan melakukan upgrade kernel terlebih dahulu. Dengan pertimbangan agar pengujian dapat dilakukan secara efektif maka penulis akan menggunakan sistem operasi yang release dengan versi kernel 3.8 untuk distribusi Ubuntu dan kernel 2.6 pada CentOS. Dengan begitu penulis bisa fokus pada pengujian tanpa harus meningkatkan versi kernel dan pengujian bisa dilakukan dengan maksimal.

Sistem operasi yang digunakan dapat dilihat pada tabel di bawa ini:

<table>
  <tr>
    <td>SISTEM OPERASI</td>
    <td>VERSI KERNEL</td> 
    <td>USER INTERFACE</td>
	<td>GUEST/HOST</td>
	<td>PENGGUNAAN</td>
  </tr>
  <tr>
    <td>CentOS 6.5</td>
    <td>2.6.32-431.el6.x86_64</td> 
	<td>Desktop</td>
    <td>Host</td>
	<td>Pengujian Cross-platform Dependencies</td>
  </tr>
<tr>
    <td>Ubuntu 14.04 LTS</td>
    <td>3.13.0-24-generic</td> 
	<td>Desktop</td>
    <td>Host</td>
	<td>Uji Efektifitas dan Kompabilitas</td>
  </tr>
<tr>
    <td>Ubuntu 14.04 LTS</td>
    <td>3.13.0-32-generic</td> 
	<td>CLI</td>
    <td>Guest</td>
	<td>Uji Kompabilitas Terhadap Perbedaan Lingkungan Host</td>
  </tr>
<tr>
    <td>Ubuntu 14.04.x (Latest)</td>
    <td>-</td> 
	<td>CLI</td>
    <td>Container</td>
	<td>Uji Efektifitas dan Kompabilitas</td>
  </tr>
<tr>
    <td>Ubuntu 12.04</td>
    <td>-</td> 
	<td>CLI</td>
    <td>Container</td>
	<td>Conflicting Dependencies</td>
  </tr>
</table>

###3.3	Topologi Jaringan

####3.3.1 Docker Registry 

Docker Registry adalah server (*public* atau private) tempat user Docker menyimpan repository untuk memudahkan *sharing* image yang telah dibuatnya.  Dalam Docker registry ini terdapat base image yang dibuat secara official, juga terdapat banyak image yang dibuat oleh pengguna Docker lain dan sangat membantu untuk dijadikan sebagai *base image* dalam proses pengembangan sebuah aplikasi. Docker registry juga mempunyai mekanisme *versioning* seperti Github dengan cara memberikan tag yang berbeda untuk repository yang sama dengan perintah `username/nama_image:tag`, contohnya:

	fahmpress/myapp:versi.1
	fahmpress/myapp:versi.2
Topologi jaringan yang dibahas pada tahap ini hanya menjelaskan hubungan host yang menjalankan Docker dengan Docker registry, yang secara implisit ini merupakan cara Docker secara *default* untuk memindahkan image yang sudah dibuat atau *dockerized app* dari satu host ke host yang lain (*shipping code*).

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.4.jpg "Gambar 3.4")

Gambar 3.4 Docker Registry

####3.3.2 Memindahkan Docker Image Melalui FTP

Selain menggunakan Docker registry, image juga bisa dipindahkan dengan menyimpan image tersebut ke dalam bentuk .tar lalu memindahkannya melalui FTP ke host yang lain.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.5.jpg "Gambar 3.5")

Gambar 3.5 Memindahkan Image Melalui FTP

###3.4 Instalasi VirtualBox dan Docker
####3.4.1 Instalasi VirtualBox dan Membuat Mesin Virtual

Sistem operasi yang digunakan untuk pengujian ini adalah Ubuntu 14.04 LTS Server. Install VirtualBox via terminal dengan menggunakan perintah:
    
    $ sudo apt-get install virtualbox
atau mendownload pada halaman resmi virtualbox https://www.virtualbox.org/wiki/Downloads dan menginstallnya secara manual. Dalam hal ini penulis mendownload virtualbox dan menginstalnya secara manual, untuk mendapatkan virtualbox dengan versi terakhir. Setelah download selesai, install virtualbox dengan perintah `dpkg -i /direktori/installer.deb`:

    $ sudo dpkg -i /Downloads/virtualbox-4.3_4.3.16-95972~Ubuntu~raring_amd64.deb

Setelah instalasi virtualbox selesai, buat virtual mesin dengan mengklik `new` pada menu lalu beri nama dan pilih sistem operasi yang akan diinstall.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.6.png "Gambar 3.6")

Gambar 3.6 Membuat mesin virtual baru

Langkah selanjutnya menentukan besaran memory yang akan digunakan oleh mesin virtual. Dalam hal ini penulis menggunakan memory sesuai dengan kebutuhan minimal untuk menjalankan OS Ubuntu yaitu 192 MB, hal ini dimaksudkan untuk meminimalkan *overhead* pada mesin host. 

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.7.png "Gambar 3.7")

Gambar 3.7 Menentukan besaran memory

Selanjutnya buat hardisk virtual dengan format VDI (*VirtualBox Disk Image*), dan memilih opsi *Dynamicallly allocated* agar penggunaan virtual hardisk efektif, ukurannya sesuai dengan besaran hardisk yang digunakan. Besaran hardisknya penulis menggunakan ukuran *default* yang diberikan oleh virtualbox yaitu 8 GB.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.8.png "Gambar 3.8")

Gambar 3.8 Menentukan besaran hardisk virtual

Agar mesin virtual mendapat koneksi internet, adapternya harus dikonfigurasi mejadi *bridge* ke adapter fisik pada mesin host.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.9.png "Gambar 3.9")

Gambar 3.9 Setingan jaringan sebagai *bridge*

Setelah itu jalankan mesin virtual dan pilih ISO file sistem operasi yang akan diinstall.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.10.png "Gambar 3.10")

Gambar 3.10 ISO installer sistem operasi

Dalam proses penginstalan sistem operasi, instalkan Open SSH server saat pemilihan paket software, untuk memudahkan mengakses terminal secara *remote* nantinya. 

####3.4.2 Instalasi Docker dan Menyiapkan Docker Image

Cara instalasi Docker berbeda pada tiap sistem operasi. Dalam hal ini penulis menggunakan sistem operasi Ubuntu 14.04 LTS, instalasi dilakukan dengan perintah berikut:

    $ sudo apt-get update
    $ sudo apt-get install docker.io
    $ sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker
    $ sudo sed -i '$acomplete -F _docker docker' /etc/bash_completion.d/docker.io

cek versi Docker dengan perintah `docker version`.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.11.png "Gambar 3.11")

Gambar 3.11 Docker versi 1.0.1

Jika versi Docker yang diinstall dari repository Ubuntu tidak update, install Docker dari repository Docker, sebelumnya pastikan sistem APT mendukung `https`. Untuk menginstallnya, tambahkan repository Docker pada `apt-source list`, lakukan update lalu install paket `lxc-docker`.

    $ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
    $ sudo sh -c "echo deb https://get.docker.io/ubuntu docker main\ > /etc/apt/sources.list.d/docker.list"
    $ sudo apt-get update
    $ sudo apt-get install lxc-docker
Cek kembali versi Docker untuk memastikan Docker yang diinstall merupakan *latest stable version*.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.12.png "Gambar 3.12")

Gambar 3.12 Docker versi 1.2.0

Setelah itu ketikan perintah berikut untuk mencoba menjalankan container Docker:

    $ sudo docker run -i -t ubuntu /bin/bash
Perintah di atas akan menjalankan container dengan *base image* Ubuntu. Docker akan mencari image ubuntu secara lokal pada Docker host, jika image belum ada Docker akan otomatis mendownload image ke registry public.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.13.png "Gambar 3.13")

Gambar 3.13 Download image ubuntu dari *public registry*

Untuk mendownload image tertentu gunakan perintah `docker pull <nama image>`. Setelah mengetikan perintah di atas, terminal akan berpindah ke terminal container yang dijalankan. Ketik `exitg` untuk keluar dari container. Lalu ketikan perintah `docker images` untuk melihat image apa saja yang ada pada repository lokal kita.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.14.png "Gambar 3.14")

Gambar 3.14 Image Docker


###3.5 *Dockerizing* Aplikasi Dengan Container Docker

Ada dua cara dalam implementasi pengembangan sebuah aplikasi web dengan menggunakan container Docker, secara manual dan menggunakan skrip. *Deployment* secara manual artinya kita membangun aplikasi dengan langkah-langkah yang kita lakukan di dalam container melalui terminal secara langsung. Sedangkan *deployment* menggunakan skrip merupakan sebuah proses otomasi (*automate build*), hal ini dilakukan dengan skrip yang disebut Dockerfile.

####3.5.1 *Dockerizing* Apache Daemon

Penulis akan membuat aplikasi web server apache menggunakan container Docker untuk pengujian yang akan dibahas pada bab selanjutnya. Base image yang digunakan adalah ubuntu:latest. Pertama jalankan container ubuntu dengan perintah berikut:

    # docker run -i -t ubuntu /bin/bash

perintah di atas akan merubah posisi terminal dari host ke dalam container. 

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.16.png "Gambar 3.16")

Gambar 3.16 Menjalankan container Docker

*Flag* `-i` mengizinkan untuk membuat koneksi interaktif, *flag* `t` memberikan sebuah pseudo-tty atau terminal di dalam container. Sedangkan `/bin/bash` adalah perintah untuk menjalankan *bash shell* di dalam container. Untuk melihat container yang sedang berjalan gunakan perintah `Docker ps` pada terminal yang lain.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.17.png "Gambar 3.17")

Gambar 3.17 Melihat container yang sedang berjalan

Setelah itu lakukan instalasi apache di dalam container.

    # apt-get update
    # apt-get -y install apache2
Sampai tahap ini docker apache web server belum bisa diakses dari luar container. Gunakan perintah `Docker Commit *<container id>* *<username/nama_image>*` untuk menyimpan perubahan pada container. Username yang digunakan disini adalah username yang digunakan untuk mengakses Docker index atau registry public. Username bisa didapatkan dengan mendaftar di halaman resmi Docker.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.18.png "Gambar 3.18")

Gambar 3.18 Menyimpan container ke dalam bentuk image

Secara *default* container yang sedang berjalan tidak bisa diakses dari luar, agar web server bisa diakses dari luar adalah dengan menggunakan *mapping* port container ke port mesin host atau istilah yang sering digunakan *Expose port*. Untuk menjalankan apache web server yang sudah dibuat sebelumnya gunakan perintah berikut:

    # docker run -p 8888:80 -d fahmpress/apache /usr/sbin/apache2ctl -D FOREGROUND
    
Perintah di atas secara explisit memerintahkan Docker untuk menjalankan apache daemon di dalam container dan memetakan port 80 di container pada port 8888 di mesin host, sehingga web server apache bisa diakses dari luar container bahkan dari luar mesin host.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.19.png "Gambar 3.19")

Gambar 3.19 Mengakses apache web server dari mesin host pada port 8888 

####3.5.2 *Dockerizing* Apache Daemon Menggunakan Dockerfile

*Deployment* container dengan dockerfile memungkinkan proses secara terdokumentasi dan mudah di *maintenance*. Untuk menggunakan dockerfile buat file dengan nama `Dockerfile` lalu masukan perintah yang sesuai dengan langkah instalasi apache. Syntax yang digunakan dalam dockerfile harus *valid* dan dikenali oleh proses `docker build` seperti FROM, MAINTENER, RUN, CMD dan lain-lain. Penulis menggunakan editor nano untuk membuat Dockerfile dengan perintah `nano Dockerfile`, lalu menulis skrip seperti berikut:

    FROM ubuntu:latest
    MAINTAINER Fahmi <persada.fahmi@gmail.com>

    RUN apt-get update && apt-get -y install apache2 && apt-get clean

    EXPOSE 80

    CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

Untuk menjalankan dockerfile gunakan perintah berikut pada direktori dimana dockerfile berada:
    
    # docker build -t fahmpress/apache2

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.20.png "Gambar 3.20")

Gambar 3.20 Membangun apache web server menggunakan dockerfile

Cek image yang telah dibuat dengan dockerfile tersebut, lalu jalankan dengan perintah:

    docker run -p 80:80 -d fahmpress/apache2

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.21.png "Gambar 3.21")

Gambar 3.21 Image yang telah dibuat dengan menggunakan dockerfile

Perintah untuk menjalankan image fahmpress/apache2 yang telah dibuat menggunakan dockerfile tidak lagi memakai argumen `/usr/sbin/apache2ctl -D FOREGROUND` seperti pada proses dockerizing apache yang dilakukan secara manual sebelumnya. Itu karena perintah untuk menjalankan daemon apache sudah diset dengan syntax CMD pada skrip dockerfile. CMD dapat menentukan apa yang akan proses oleh container saat dijalankan dengan perintah `docker run`. Akses web apache yang telah dibuat dengan menggunakan browser pada mesin host.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.22.png "Gambar 3.22")

Gambar 3.22 Mengakses apache web server dari mesin host pada port *default* http

Pada repository Docker Registry banyak terdapat image dan dockerfile sebagai *builder* yang bisa digunakan sebagai *base image* untuk aplikasi web server, agar pembuatan web server bisa lebih mudah dan efektif. Untuk pengujian 3 variasi uji kompabilitas Docker, penulis membangun aplikasi web menggunakan Dockerfile dari repository tutum/lamp pada Docker registry.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.23.png "Gambar 3.23")

Gambar 3.23 Repository tutum/lamp pada Docker Index Registry

Penulis menggunakan Dockerfile dari tutum/lamp dengan modifikasi pada aplikasi PHP-nya. Aplikasi web server PHP menggunakan *source code* PHP yang disipakan penulis pada repository Github.