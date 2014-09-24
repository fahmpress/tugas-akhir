##BAB III - PERANCANGAN DAN IMPLEMENTASI


###3.1	Skenario Pengujian 

Pengujian dilakukan untuk menguji keunggulan Dokcer dalam hal proses *deployment* yang dianggap bisa mengatasi kekurangan pada virtualisasi sebelumnya menggunakan mesin virtual tradisional. Selain itu, pengujian dilakukan juga untuk menjawab permasalahan yang sering terjadi dalam pengembangan aplikasi web. Untuk menjawab hal tersebut, dalam penulisan ini akan dibahas mengenai skenerio dan metode pengujiannya. 

####3.1.1	Uji Efektifitas Docker Dalam Penggunaan Sumber Daya
Docker merupakan Platform as a Service yang menggunakan teknologi virtualisasi yang lebih maju dari virtualisasi sebelumnya, sehingga virtualisasi sebelumnya disebut sebagai virtualisasi tradisional. Untuk itu, teknologi virtualisasi ini dijadikan sebagai bahan analisa untuk membandingkan kinerja teknologi virtualisasi Docker dengan virtualisasi tradisional. Untuk membandingkan kinerja dan penghematan sumber daya ini akan di ambil parameter uji sebagai berikut :

#####3.1.1.1	Penghematan Penyimpanan (*Storage*)
1. Union File System

Dalam Linux boot tradisional, kernel pertama kali menggunakan (*mount*) *root file system* sebagai *read-only*, memeriksa integritasnya, lalu mengganti keseluruhan `rootfs` menjadi mode *read-write*.

Sama seperti Linux boot tradisional, `rootfs` pada Docker akan di-*mount* pertama kali dalam mode *read-only*, namun kemudian, tidak merubah file system menjadi mode *read-write*, Docker mengambil keuntungan dari *union mount* untuk menambah file system *read-write* di atas file system read-only*. Hasilnya, akan ada beberapa file system *read-only* ditumpuk di atasnya satu sama lain. 

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.1.jpg "Gambar 3.1")

Gambar 3.1 File system as a Layer

Pertama kali, tidak ada apa-apa pada lapisan *read-write* paling atas, namun kapan saja berjalan sebuah proses akan menghasilkan sebuah file, hal ini terjadi pada lapisan di atasnya. Dan jika sesuatu memerlukan *update* pada file yang berada di lapisan lebih rendah, maka file akan disalin ke lapisan yang lebih atas dan perubahan berbentuk sebuah salinan. Versi file di lapisan di bawahnya tidak bisa lagi terlihat oleh aplikasi, padahal sebenarnya ada, dan tidak berubah.

Mekanisme file system yang menjadi *back-end* container Docker ini disebut **Union File System**. Hal inilah yang menjadikan proses *deployment* container Docker menjadi efektif dalam hal penyimpanan dibanding dengan mesin virtual tradisional seperti VirtualBox, Docker tidak akan membuat snapshot dengan menyalin seluruh file sistem yang ada sebagai image, namun hanya menyalin lapisan perubahannya saja.

2. Metode Uji dengan Studi Komparasi

Sesuai paparan di atas terlihat perbedaan penggunaan penyimpanan Docker dengan mesin virtual tradisional. Dalam hal ini penulis akan melakukan pembuktian hipotesa tersebut dengan melakukan komparasi antara Docker dan VirtualBox, sehingga terlihat efektifitas Docker dibandingkan mesin virtual tradisional.

Untuk malakukan pengujian tersebut penulis akan menginstall Docker dan VirtualBox pada mesin host dan sistem operasi yang sama secara bergantian agar hardware yang digunakan identik dan sama persis, hal ini dilakukan atas pertimbangan integritas pengujian. Lalu menjalankan satu mesin virtual (container) dan melakukan 2 proses yang masing-masing proses akan diambil snapshot-nya. Parameter uji yang digunakan dalam pengujian ini adalah besaran penggunaan penyimpanan (*storage*)

#####3.1.1.2.	Penghematan Memory
Dalam proses deployment-nya Docker container menggunakan shared kernel dari mesin host tanpa ada perantara lapisan virtualisasi seperti *hypervisor*, maka proses menjadi lebih ringan sehingga bisa menghemat memory dan overhead pada mesin host (*zero overhead*) sehingga memungkinkan untuk menjalankan banyak container dalam satu mesin, berbeda dengan virtualisasi tradisional yang menggunakan *hypervisor* dan kernel tersendiri dari mesin host.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.2.jpg "Gambar 3.2")

Gambar 3.2 Shared Host Kernel pada Docker

Untuk pengujian ini akan dilakukan komparasi saat proses *deployment* mesin virtual (container) antara Docker dan VirtualBox. Docker dan Virtualbox akan diinstal pada mesin host dan sistem operasi yang sama. Setelah itu akan dijalankan beberapa mesin virtual dan container lalu akan dilihat penggunaan memorynya. Pengukuran memory akan menggunakan htop. Parameter uji dalam pengujian ini adalah besaran kenaikan memory yang digunakan saat menjalankan mesin virtual atau container.

####3.1.2	Uji Kompabilitas Docker

Aplikasi yang sudah diinstall, dipaketkan dan dijalankan menggunakan container Docker disebut *Dockerized app*, Docker mengklaim sekali *developer* software membangun aplikasi dengan container, maka *dockerized app* bisa dijalankan di hampir semua *environment* seperti virtual mesin, Laptop, cloud, bare metal, dan lain-lain. Dalam hal ini penulis akan menguji hal tersebut dengan menjalankan *dockerized app* pada *environment* yang berbeda termasuk kompabilitas dengan lingkungan host yang mempunyai masalah *conflicting dependencies*.

#####3.1.2.1	Uji Kompabilitas Container Docker Terhadap Perbedaan Platform

1. *Cross-platform Dependencies*

Idealnya, developer aplikasi harus mampu membuat aplikasi yang fleksibel yang mampu dijalankan lintas platform untuk dapat menangani kasus seperti migrasi server ke server lain dengan sistem operasi yang berbeda. Namun pada kenyataannya hal ini sulit untuk diimplementasikan karena ketergantungan aplikasi terhadap suatu platform atau permasalahan yang biasa disebut *cross-platform dependencies*, dimana *sysadmin* harus mengkonfigurasi ulang *environment* baru untuk aplikasinya karena perbedaan sistem operasi server dan versi kernel.

Docker menjawab permasalahan tersebut dengan containernya. Aplikasi yang sudah di-*package* menjadi *dockerized app* bersama semua *dependencies*-nya menggunakan container akan mampu berjalan pada platform yang menjalankan Docker (*enable dokcer engine*) tanpa harus merubah dan mengkonfigurasi apapun pada container ataupun mesin host.

2.	Metode Pengujian

Pengujian akan dilakukan dengan metode simulasi (virtual mesin sebagai mesin host untuk Docker) dengan menginstall Web server pada 2 mesin virtual yang masing-masing menggunakan sistem operasi Linux yang berbeda distro (Ubuntu 14.04 dan CentOS 7). Web server akan diinstall dengan menggunakan container pada mesin Ubuntu, lalu *dockerized* web server tersebut akan dijalankan di mesin CentOS tanpa melakukan perubahan apapun pada mesin host ataupun container.

#####3.1.2.2 Uji Kompabilitas Container Docker Terhadap Perbedaan Hardware

1.	Pentingnya Fleksibilitas Aplikasi

Contoh kasus, dalam pengembangan aplikasi dengan skala *enterprise* seperti pada perusahaan bisnis, aplikasi yang dikembangkan sebagai servis yang dijalankan untuk *customers* harus memenuhi standar mutu dan spesifikasi yang dibutuhkan perusahaan. Untuk itu aplikasi yang telah dibangun oleh *developer* pada mesin lokalnya (semisal Laptop) akan diuji kelayakannya pada hardware Quality Assurance (QA Server). QA Server akan melakukan validitas untuk memastikan aplikasi tersebut memenuhi spesifikasi QC (*Quality Control*) dan menguji fitur serta fungsionalitasnya agar sesuai dengan sasaran pelaku bisnis. Setelah itu aplikasi akan dijalankan (di-*hosting*) pada hardware yang berbeda pula, misalnya Cloud (*Private/Public*), bare metal, virtual server, virtual mesin, dan sebagainya.

Pada kasus diatas, aplikasi harus mempunyai fleksibilitas tinggi agar mampu dijalankan pada hardware yang berbeda, hal ini dimaksudkan untuk menghindari kesalahan atau error saat melakukan re-*packaging dependencies* dan konfigurasi yang dibutuhkan oleh aplikasi tersebut. Dengan Docker hal itu tidak akan menjadi permasalahan yang berarti selama hardware support untuk menjalankan Docker engine. Docker memastikan lingkungan host tidak akan berpengaruh pada container dan lingkungan container akan sama persis seperti saat dimana dia dibuat. Oleh karena itu *Dockerized app* yang sudah dibangun akan mampu dijalankan dimanapun yang menjalankan Docker engine tanpa harus melakukan perubahan apapun.

2.	Metode Pengujian

Penulis akan menjalankan *Dockerized app* pada hardware yang berbeda, yaitu hardware Laptop dan virtual mesin yang menggunakan metode virtualisasi penuh (virtual hardware). Tentu saja ini merupakan *environemnt* (laptop dan mesin virtual) yang berbeda, karena virtual mesin yang menggunakan metode virtualisasi penuh bersifat independent dan terpisah dari mesin host. Pada realitasnya hal ini bisa terjadi pada saat aplikasi dijalankan oleh perusahaan yang melakukan konsolidasi server dengan virtualisasi seperti XEN dan VMWare.

#####3.1.2.3 Uji Kompabilitas Container Docker Terhadap Perbedaan Versi Aplikasi

###3.2	Pemilihan Software dan Sistem Operasi

Sesuai skenerio pengujian di atas, jumlah variasi pengujian adalah 5 variasi pengujian. Untuk melakukan pengujian tersebut penulis menggunakan software dan sistem operasi Linux dengan distribusi yang berbeda.

####3.2.1	Pemilihan Software

Untuk pengujian dengan variasi yang sudah disebutkan penulis memilih software aplikasi berbasis web yang masih banyak digunakan saat ini terutama di Indonesia seperti LAMP server yang digunakan untuk membuat server web.

1.	Apache
2.	

####3.2.2	Pemilihan Sistem Operasi

Docker hanya bisa berjalan pada kernel yang sudah ditentukan yaitu 3.8 ke atas, namun sistem operasi yang memiliki kernel dibawahnya tetap bisa menjalankan Docker dengan melakukan upgrade kernel terlebih dahulu. Dengan pertimbangan efektifitas dalam pengujian maka penulis akan menggunakan sistem operasi yang release dengan versi kernel terbaru (3.8 atau lebih). Dengan begitu penulis bisa fokus pada pengujian tanpa harus meningkatkan versi kernel dan pengujian bisa dilakukan dengan maksimal.
Pengecualian untuk variasi uji penghematan memory dan penyimpanan, penulis akan membandingkan kinerja dua mesin menggunakan sistem operasi Proxmox dengan versi kernel 2.6, penulis akan membuat 2 mesin virtual dengan sistem operasi Proxmox dengan versi kernel yang berbeda.

###3.3	Topologi Jaringan


`last edited: 9/23/2014 2:04:01 PM`