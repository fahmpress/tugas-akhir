##BAB II - LANDASAN TEORI


###2.1	Cloud Computing
###2.1.1	Definisi Cloud Computing 

Cloud computing adalah gabungan pemanfaatan teknologi komputer dan pengembangan berbasis Internet. Awan (cloud) adalah metafora dari internet, sebagaimana awan yang sering digambarkan di diagram jaringan komputer. Sebagaimana awan dalam diagram jaringan komputer tersebut, awan (cloud) dalam Cloud Computing juga merupakan abstraksi dari infrastruktur kompleks yang disembunyikannya. Ia adalah suatu metoda komputasi di mana kapabilitas terkait teknologi informasi disajikan sebagai suatu layanan (as a service), sehingga pengguna dapat mengaksesnya lewat Internet ("di dalam awan") tanpa mengetahui apa yang ada didalamnya, ahli dengannya, atau memiliki kendali terhadap infrastruktur teknologi yang membantunya.

Komputasi awan adalah suatu konsep umum yang mencakup SaaS, Web 2.0, dan tren teknologi terbaru lain yang dikenal luas, dengan tema umum berupa ketergantungan terhadap Internet untuk memberikan kebutuhan komputasi pengguna. Jenis layanan dalam Cloud computing ini ada tiga macam yang berupa infrastruktur, platform dan software.

 
![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar2.1.jpg "Gambar 2.1")

Gambar 2.1 Model layanan Cloud Computing

####2.1.2	Layanan Cloud Computing

######1.	Software as a Service
Software as a Service adalah layanan Cloud computing dimana kita bisa langsung menggunakan aplikasi yang telah disediakan. Penyedia layanan mengelola infrastruktur dan platform yang menjalankan aplikasi tersebut. Contoh layanan aplikasi email yaitu gmail, yahoo dan outlook sedangkan contoh aplikasi media sosial adalah twitter, facebook dan google+. Keuntungan dari layanan ini adalah pengguna tidak perlu membeli lisensi untuk mengakses aplikasi tersebut. Pengguna hanya membutuhkan perangkat klien komputasi awan yang terhubung ke internet. Ada juga aplikasi yang mengharuskan pengguna untuk berlangganan agar bisa mengakses aplikasi yaitu Office 365 dan Adobe Creative Cloud.
######2.	Platform as a Service
Platform as a Service adalah layanan yang menyediakan computing platform. Biasanya sudah terdapat sistem operasi, database, web server dan framework aplikasi agar dapat menjalankan aplikasi yang telah dibuat. Perusahaan yang menyediakan layanan tersebutlah yang bertanggung jawab dalam pemeliharaan computing platform ini. Keuntungan layanan PaaS ini bagi pengembang adalah mereka bisa fokus pada aplikasi yang mereka buat tanpa memikirkan tentang pemeliharaan dari computing platform. Contoh penyedia layanan PaaS adalah Amazon Web Service dan Windows Azure.
######3.	Infrastructure as a Service
Infrastructure as a Service adalah layanan Cloud computing yang menyediakan infrastruktur IT berupa CPU, RAM, storage, bandwith dan konfigurasi lain. Komponen-komponen tersebut digunakan untuk membangun komputer virtual. Komputer virtual dapat diinstal sistem operasi dan aplikasi sesuai kebutuhan. Keuntungan layanan IaaS ini adalah tidak perlu membeli komputer fisik sehingga lebih menghemat biaya. Konfigurasi komputer virtual juga bisa diubah sesuai kebutuhan. Misalkan saat storage hampir penuh, storage bisa ditambah dengan segera. Perusahaan yang menyediakan IaaS adalah Amazon EC2, TelkomCloud dan BizNetCloud.
 
####2.1.3	Model Deployment

######1.	Private Cloud
Private Cloud adalah infrastruktur yang dioperasikan semata-mata hanya untuk sebuah organisasi, apakah diatur secara internal atau oleh pihak ketiga, dan dihosting baik secara internal atau external. Membangun sebuah projek private cloud memerlukan tingkat significan dan tingkat keterlibatan untuk memvirtualkan lingkungan bisnis, dan membutuhkan organisasi untuk melakukan evaluasi ulang tentang sumber daya yang sudah ada. Ketika sudah dilakukan dengan benar, hal itu bisa meningkatkan bisnis, namun setiap langkah dalam projek menimbulkan masalah keamanan yang harus diatasi untuk menjaga kelemahan yang serius.
######2.	Public Cloud
Sebuah cloud dinamakan “public cloud” ketika layanan diberikan melalui jaringan yang terbuka untuk penggunaan publik. Layanan public cloud bisa gratis atau ditawarkan dalam model pay-per-usage (dibayar sesuai penggunaan). Secara teknis hampir tidak ada perbedaan antara arsitektur public dan private cloud, namun, pertimbangan keamanan mungkin berberbeda secara substansial untuk layanan (aplikasi, storage, dan sumber daya yang lain) yang disediakan oleh provider layanan untuk pengguna publik dan ketika komunikasi dipengaruhi oleh jaringan yang tidak dipercaya. Secara umum, penyedia layanan public cloud seperti Amazon AWS, Microsoft dan Google memiliki dan mengoprasikan infrastruktur di data center mereka sendiri dan akses umumnya melalui internet. 
######3.	Hybrid Cloud
Hybrid cloud adalah komposisi dari dua atau lebih model cloud (private, community atau public) yang terdiri dari entitas berbeda namun terikat bersama, menawarkan keuntungan berbagai model deployment. Hybrid cloud juga dapat brarti sebuah kemampuan untuk menghubungkan kolokasi, diatur dan/atau layanan dedicated dengan sumber daya cloud.
Perusahaan Gartner, Inc. menjelaskan sebuah layanan hybrid cloud sebagai layanan cloud computing yang terdiri atas beberapa kombinasi dari private, public dan community layanan cloud, dari penyedia layanan yang berbeda. Sebuah hybrid cloud melintasi isolasi dan batas provider (penyedia) jadi tidak bisa disimpulkan sebagai satu kategori layanan private, public, atau community cloud. Hal itu memungkinkan satu untuk memperluas baik kapasitas atau kemampuan layanan cloud, dengan agregasi, integrasi atau modifikasi dengan layanan cloud yang lain.
Ada beberapa variasi dalam kasus penggunaan hybrid cloud. Contohnya, sebuah organisasi menyimpan data klien yang sensitive pada aplikasi private cloud, tapi mengkoneksikan aplikasi tersebut ke aplikasi bisnis pada public cloud sebagai layanan software. Berikut adalah contoh dari hybrid cloud yang memperluas kemampuan perusahaan untuk memberikan layanan bisnis yang spesifik melalui penambahan secara external tersedia layanan public cloud.
 
###2.2	Virtualisasi
####2.2.1	Definisi Virtualisasi
Virtualisasi adalah istilah umum yang mengacu kepada abstraksi dari sumber daya komputer. Definisi lainnya adalah sebuah teknik untuk menyembunyikan karakter fisik dari sumber daya komputer dari bagaimana cara sistem lain, aplikasi atau pengguna berinteraksi dengan sumber daya tersebut. Hal ini termasuk membuat sebuah sumber daya tunggal seperti server, sebuah sistem operasi, sebuah aplikasi, atau peralatan penyimpanan terlihat berfungsi sebagai beberapa sumber daya logikal, atau dapat juga termasuk definisi untuk membuat beberapa sumber daya fisik (seperti beberapa peralatan penyimpanan atau server) terlihat sebagai satu sumber daya logikal.
Melihat catatan sejarah istilah virtualisasi mulai dikembangkan sejak pertengahan abad kek 20 dimana hanya digunakan untuk kalangan industry saja. 

####2.2.2	Kenapa Virtualisasi
Virtualisasi menawarkan banyak keuntungan dibanding infrastruktur tradisional dalam berbagai aplikasi. Selain dari meningkatkan utilitas mesin host melalui konsolidasi server juga menawarkan banyak sisi manfaat. Kisaran keuntungan ini dari mengurangi biaya fiskal sampai kemudahan pengelolaan dan deployment sistem tambahan pada infrastruktur virtual. Banyak produk virtualisasi memungkinkan guest tertentu untuk diduplikasi dengan mudah dimana bisa berguna untuk percobaan bagaimana perangkat lunak diperbaharui atau dimodifikasi bisa merubah sebuah sistem yang ditentukan tanpa mempengaruhi sistem produksi. Migrasi online atau offline sangat berguna dalam kejadian sebuah fisikal host tertentu memerlukan upgrade atau penggantian. Migrasi membantu menurunkan atau mengurangi downtime karena mesin virtual bisa di pindahkan secara sementara atau permanen ke host transparan yang berbeda ke sistem operasi guest.Usaha pemulihan dari bencana (Disaster Recovery) bisa menjadi benar-benar sederhana melalui penggunaan virtualisasi. Dalam sebuah kejadian bencana alam, backup mesin virtual mesin bisa dengan mudah dipindahkan ke lokasi baru pada hardware yang berbeda membantu meminimalisir downtime.

Walaupun dengan semua keuntungan masih terdapat beberapa sisi kekurangan pada virtualisasi. Contohnya, mesin virtual harus membagi sumber daya dengan mesin virtual yang lain dalam sistem fisikal yang sama. Aplikasi dengan penyimpanan atau utilitas CPU tinggi tidak selalu bekerja dengan baik dalam sebuah sistem dimana mesin virtual itu harus membagi sumber daya. Permasalahan ini bisa dihindari dengan hanya menjalankan satu dari semua aplikasi dengan utilitas tinggi per host fisikal.

####2.2.3	Komponen Virtualisasi
#####2.2.2.1	Hypervisor
Hypervisor, juga dikenal sebagai Virtual Machine Monitor (VMM) adalah lapisan perangkat lunak yang memungkinkan adanya virtualisasi. Hypervisor bertanggungjawab membuat lingkungan virtual dimana mesin virtual guest beroprasi. Hypervisor mengontrol sistem guest dan memastikan sumber daya dialokasikan ke mesin guest sesuai yang dibutuhkan. Secara umum hypervisor diklasifikasikan menjadi dua kategori; tipe 1 dan tipe 2.
 
![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar2.2.jpg "Gambar 2.2")

Gambar 2.2 Kedudukan Hypervisor 

1.	Hypervisor Tipe 1
Hypervisor berjalan langsung di hardware server tanpa perantara sistem operasi. Karena tidak ada intervensi layer antara hypervisor dan hardware fisikal, hypervisor tipe ini juga dikenal sebagai implementasi bare-metal. Tanpa perantara, hypervisor type 1 ini bisa secara langsung berkomunikasi dengan sumber daya hardware.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar2.3.jpg "Gambar 2.3")

Gambar 2.3 Hypervisor Tipe 1

2.	Hypervisor Tipe 2
Hypervisor tipe ini sendiri adalah merupakan sebuah software yang berjalan di atas sebuah sistem operasi. Sistem operasi yang sebenarnya (host OS) menangani seluruh sumber daya hardware dan hypervisor memanfaatkan kemampuan itu.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar2.4.jpg "Gambar 2.4")
 
Gambar 2.4 Hypervisor Tipe 2

#####2.2.2.2	Guest
Guest, baik sebuah aplikasi atau sistem operasi, adalah apa yang dijadikan virtual di atas hypervisor. Dalam beberapa kasus sebuah sistem operasi bisa untuk berjalan native dan berubah dalam hypervisor tentunya diketahui itu divirtualkan. Dalam kasus lain, tergantung pada hypervisor, sistem operasi guest membutuhkan driver tertentu atau didesain secara spesifik untuk berjalan di atas hypervisor.


####2.2.4	Tipe Virtualisasi
#####2.2.4.1	Virtualisasi Perangkat Keras
Virtualisasi perangkat keras atau virtualisasi platform mengacu pada upaya menciptakan mesin virtual yang bekerja layaknya sebuah komputer lengkap dengan sistem operasi. Software yang dieksekusi pada mesin virtual tersebut dipisahkan dari sumber daya fisik. Dalam virtualisasi perangkat keras, mesin host adalah mesin dimana virtualisasi itu berada, dan mesin guest adalah mesin virtual itu sendiri. Istilah host dan guest digunakan untuk membedakan software yang berjalan di mesin fisik dari software yang berjalan di mesin virtual. 
Jenis virtualisasi perangkat keras meliputi :

1.	Virtualisasi Penuh
Hampir menyerupai mesin asli dan mampu menjalankan perangkat lunak (Sistem Operasi) tanpa perlu diubah.
2.	Virtualisasi Sebagian
Tidak semua aspek lingkungan disimulasikan dan tidak semua perangkat lunak dapat langsung berjalan, beberapa perlu disesuaikan untuk dapat berjalan dalam lingkungan virtual ini.
3.	Para-Virtualisasi
Perangkat keras tidak disimulasikan tetapi perangkat lunak guest berjalan dalam domainnya sendiri seolah-olah dalam sistem yang berbeda. Dalam hal ini perangkat lunak guest perlu disesuaikan untuk dapat berjalan.

#####2.2.4.2	Virtualisasi Perangkat Lunak
Virtualisasi perangkat lunak memungkinkan satu komputer host untuk membuat dan menjalankan satu atau lebih lingkungan virtual. Virtualisasi software banyak digunakan untuk mensimulasikan sebuah sistem komputer lengkap dengan tujuan untuk memungkinkan sistem operasi guest berjalan, sebagai contoh mengizinkan Linux untuk berjalan sebagai guest diatas komputer yang secara native menjalankan sistem operasi Windows. Jenis virtualisasi perangkat lunak diantaranya adalah Operating sistem-level virtualization.

####2.2.5	Operating sistem-level virtualization
Operating system-level virtualization adalah sebuah metode virtualisasi server dimana kernel dari sebuah system operasi mengijinkan beberapa user space instance yang terisolasi, dari pada hanya satu. Instance tersebut (sering disebut sebagai container, virtualization engines (VE), virtual private server (VPS) atau jails) terlihat dan terasa seperti server asli dari sudut pandang pengguna.

Dalam system operasi Unix-like, teknologi ini bisa terlihat dengan implementasi lanjut dengan standard mekanisme chroot. Selain itu untuk isolasi mekanisme, kernel sering mendukung fiture management sumber daya untuk membatasi dampak dari satu aktifitas container ke container lain.

Bentuk virtualisasi ini biasanya ringan dan tanpa overhead, karena program dalam partisi virtual menggunakan system operasi normal system call interface dan tidak membutuhkan untuk tunduk untuk mengemulasi atau menjalankan sebuah virtual mesin antara, seperti contoh kasus whole-system virtualizer (seperti VMware ESXi dan QEMU) atau paravirtualizers (seperti Xen dan UML). 

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar2.5.jpg "Gambar 2.5")

Gambar 2.5 Perbandingan OS-level Virtualization dengan Virtualisasi 
perangkat keras

Operating system-level virtualization membagi sumber daya mesin fisikal pada level sisetm operasi. Ini artinya semua mesin virtual OS-level membagi satu kernel pada sebuah sistem operasi. Gambar 2.5 membandingkan lapisan virtualisasi OS-level virtualization dengan virtualisasi hardware (hardware-level virtualization). 

Contoh implementasi dari operating system-level virtualization ini adalah LXC dan Docker.

###2.3	LXC
LXC (LinuX Containers) adalah sebuah metode virtualisasi operating system-level virtualization untuk menjalankan beberapa sistem Linux yang terisolasi (container) dalam sebuah control host.

Linux kernel meliputi cgroups untuk mengisolasi sumber daya (CPU, memory, block I/O, network, dan lain-lain) yang tidak harus menjalankan mesin virtual apapun. Cgroup juga mendukung isolasi namespace untuk benar-benar mengisolasi lingkungan operasi proses aplikasi, termasuk proses trees, network, user ids dan mounted file systems.

LXC menggabungkan dukungan cgroup dan namespace untuk mendukung sebuah lingkungan yang terisolasi sebuah aplikasi. Docker juga bisa menggunakan LXC sebagai salah satu  dari execution drivers, memungkinkan manajemen image dan mendukung layanan deployment.

###2.4	Docker
Docker adalah sebuah projek open-source yang mengotomasi pegerjaan sebuah aplikasi di dalam software container, demikian itu mendukung lapisan tambahan dari abstraksi dan otomasi sebuah operating system-level virtualization dalam linux. Docker menggunakan fitur isolasi sumber daya dari kernel linux seperti cgruops dan namespaces untuk menginjinkan container secara independen untuk berjalan di dalam satu contoh linux, menghindari overhead ketika menjalankan mesin virtual. 

Namespaces Linux kernel sepenuhnya mengisolasi lingkungan operasi sebuah proses aplikasi, termasuk proses trees, network, user IDs dan mounted file systems, sementara cgroups mendukung isolasi sumber daya, termasuk CPU, memory, block I/O dan jaringan. Docker berisi libcontainer library sebagai acuan implementasi untuk container, dan membangun di atas libvirt, LXC (Linux Container) dan system-nspawn, yang mendukung antar muka pada dukungan fasilitas dengan Linux kernel.
Menurut penelitian industry analyst firm 451, “Docker adalah sebuah tool yang bisa mem-package sebuah aplikasi bersama dependency-nya dalam sebuah virtual container dan dapat berjalan di server Linux apapun. Hal ini membantu flexibilitas dan portabilitas dimana aplikasi bisa dijalankan, apakah di public/private cloud, bare metal, dan lain-lain.

####2.4.1	Kelebihan Docker dari Mesin Virtual Tradisional
Metode yang biasa digunakan untuk menidstribusikan aplikasi dan mengisolasi eksekusinya adalah menggunakan virtual mesin atau VMs. Format virtual mesin biasanya adalah VMWare’s vmdk, Oracle Virtualbox’x vdi, dan Amazon EC2’s ami. Secara teori format tersebut akan mengijinkan setiap developer secara otomatis mem-package aplikasinya ke dalam sebuah “mesin” untuk kemudahan distribusi dan deployment. Namun praktiknya, hal itu hampir tidak terjadi karena beberapa alasan :

1.	*Size* : Mesin virtual sangat besar yang membuatnya tidak praktis untuk disimpan dan dipindahkan.
2.	*Performance* : Menjalankan mesin virtual mengkonsumsi CPU dan memory secara signifikan, yang membuatnya tidak praktis di banyak scenario, contohnya pengembangan aplikasi lokal multi-tier, dan deployment CPU dan aplikasi intensif memory skala besar dalam jumlah mesin yang banyak.
3.	*Portability* : Membandingkan lingkungan virtual mesin tidak berjalan baik satu sama lain, walaupun tool konversi ada, tapi mereka terbatas dan menambah lebih banyak overhead.
4.	*Hardware-centric* : Virtual mesin didesain dengan operator mesin, bukan pengembang software. Hasilnya, mereka menawarkan peralatan yang sangat terbatas untuk apa yang sering dibutuhkan oleh pengembang; membangun, mengetest dan menjalankan software-nya. Sebagai contoh, penawaran virtual mesin tanpa fasilitas untuk versioning aplikasi, monitoring, konfigurasi, logging atau layanan discovery.

Sebaliknya, Docker memakai metode sandboxing berbeda, yang dikenal sebagai containerization. Tidak seperti virtualisasi tradisional, containerization mengambil tempat pada level kernel. Banyak sistem kernel sistem operasi modern saat ini yang mendukung kebutuhan sederhana untuk contenerization, termasuk Linux dengan OpenVZ, vserver, LXC, Solaris dengan Zones dan FreeBSD dengan Jails.
Docker dibangun di atas primitif low-level tersebut untuk menawarkan developer sebuah format portable dan lingkungan runtime yang memecahkan 4 masalah di atas. Docker container sangat kecil (dan perpindahannya bisa dioptimalkan dengan layers), Docker pada dasarnya memiliki nol overhead memory dan CPU, Docker benar-benar portable dan didisain dari dasar dengan disain application-centric. Virtual mesin baik digunakan untuk mengalokasikan sumber daya hardware, container beroperasi pada level proses, yang membuatnya sangat ringan dan sempurna sebagai unit pendistribusi software. Bagian terbaik adalah, karena Docker beroperasi pada level OS, maka Docker masih bisa berjalan di dalam mesin virtual.

####2.4.2	Kelebihan Docker dari LXC
Docker bukan bukan sebuah pengganti untuk LXC. LXC mengacu pada kemampuan kernel Linux (terutama namespace dan control groups) yang memungkinkan sandboxing satu proses dari yang lain, dan mengatur alokasi sumber daya. Di atas fondasi level bawah dari fitur kernel ini, Docker menawarkan high-level tool dengan beberapa fungsional yang powerful :

1.	*Portable deployment across machines*

Docker menentukan format untuk mem-bundle sebuah aplikasi beserta semua dependency-nya kedalam sebuah objek yang bisa didistribusikan ke mesin yang menjalankan Docker (Docker-enable machine), dan mengeksekusinya dengan jaminan bahwa lingkungan tempat mengeksekusi aplikasi akan sama. LXC mengimplementasikan proses sandboxing, yang merupakan prasyarat penting untuk deployment yang portable, namun tidak cukup hanya deployment yang portable. Jika kita mengirimkan sebuah salinan aplikasi yang diinstall pada sebuah LXC dengan konfigurasi custom, itu hampir tidak akan berjalan pada mesin yang lain seperti berjalan pada mesin sebelumnya, karena itu terikat dengan mesin sebelumnya dimana aplikasi itu dibangun dengan konfigurasi tertentu; jaringan, penyimpanan, logging, distro, etc. Docker mempunyai sebuah abstraksi untuk pengaturan mesin secara spesifik, jadi Docker container yang sama persis bisa berjalan, tanpa harus dirubah pada banyak mesin yang berbeda, dengan banyak konfigurasiyang berbeda.

2.	*Application-centric*

Docker dioptimalkan untuk deployment sebuah aplikasi, sebagai lawan mesin. Hal ini direpleksikan pada API, user interface, disain filosofi dan dokumentasinya. Sebaliknya, script pembantu LXC fokus pada container sebagai mesin yang ringan, pada dasarnya server yang booting lebih cepat dan mengurangi penggunaan RAM. Developer Docker berfikir ada lebih banyak untuk container dari pada itu.

3.	*Versioning*

Docker mempunyai kemampuan git-like untuk melacak urutan versi dari sebuah container, memeriksa diff diantara versi, membuat versi baru, rolling back, dan lain-lain. Hystori juga terdapat pada container, bagaimana sebuah container dirakit dan oleh siapa, jadi kita mempunyai kemampuan melacak secara penuh dari server produksi sepanjang perjalanan kembali ke upstream developer. Docker juga mengimplementasikan incremental upload dan download, mirip seperti git pull, jadi versi baru sebuah container bisa ditransfer dengan hanya mengirimkan diffs.

4.	*Component re-use*

Semua container bisa digunakan sebagai “base image” untuk membuat komponen yang lebih spesifik. Hal ini bisa dilakukan manual atau sebagai sebuah pembangunan secara otomatis. Contohnya, kita bisa menyiapkan lingkungan Python yang ideal, dan menggunakannya sebagai dasar dari 10 aplikasi yang berbeda. Atau konfigurasi idel Postgresql bisa digunakan kembali (re-use) untuk semua project di masa yang akan dating, dan seterusnya.

5.	*Sharing*

Docker mempunyai akses ke sebuah public registry dimana ribuan orang telah meng-upload container yang berguna; apapun dari Redis, CouchDB, untuk beberapa distro Linux. Registry juga memiliki sebuah “standard library” untuk container yang bermanfaat dan dirawat secara resmi oleh team Docker. Registry itu sendiri adalah open-source, jadi setiap orang bisa membangun registry mereka sendiri untuk menyimpan dan mendistribusikan private container, untuk deployment server internal contohnya.

6.	*Tool Ecosystem*

Docker memiliki sebuah API untuk mengotomasi dan meng-custom pembuatan dan deployment sebuah container. Ada banyak tool yang berintegrasi dengan Docker untuk megembangkan kemampuannya. Deployment PaaS (Dokku, Deis, Flynn), multi-node orchestration (Maestro, Salt, Mesos, Openstack Nova), management dashboards (docker-ui, Openstack Horizon, Shipyard), managemen konfigurasi (Chef, Puppet), continuous integration (Jenkins, Strider, Travis) dan lain-lain. Docker dengan cepat menetapkan diri sebagai standar untuk tool berbasis container.
 
###2.5	Dependency Hell
Dependency hell istilah yang mencerminkan sebuah kondisi frustasi pengguna software yang telah menginstall paket software yang memiliki ketergantungan pada versi tertentu dari paket software yang lain.

Permasalahan ketergantungan timbul dikisaran shared package/library dimana beberapa paket lain memiliki dependensi tetapi tergantung pada perbedaan dan versi yang tidak kompatibel dari sebuah shared packages. Jika shared package/library hanya bisa diinstall menjadi satu versi, pengguna atau administrator akan perlu untuk mengatasi permasalahan yang didapat dari versi lama/baru dari paket ketergantungan. Hal ini pada gilirannya, akan merusak dependensi lain dan mendorong masalah ke set paket yang lain, demikianlah istilah hell.

Permasalahan umum bagi developer adalah sulitnya mengelola semua dependency aplikasi dalam sebuah cara otomasi yang sederhana. Hal ini merupakan bentuk dari dependency hell tersebut diatas. Contoh permasalahan dependency hell yang disebutkan oleh developer Docker ada 3 yaitu Cross-platform dependencies, conflicting dependencies dan Custom dependencies.

####2.5.1	Cross-platform Dependencies
Aplikasi modern sering kali bergantung pada kombinasi sistem library dan binary, paket bahasa yang spesifik, modul framework spesifik, komponen internal yang dikembangkan untuk projek lain, dan lain-lain. Dependencies tersebut hidup pada dunia yang berbeda dan memerlukan tools yang berbeda, tools tersebut biasanya tidak bekerja dengan baik antara satu dan lainnya, membutuhkan integrasi perubahan yang janggal.

####2.5.2	Conflicting Dependencies
Aplikasi yang berbeda akan bergantung pada versi yang berbeda dalam satu dependency. Packaging tools mengatasi situasi tersebut dengan berbagai tingkat kemudahan, namun kesemua itu mengatasinya dengan berbeda dan cara yang tidak kompatibel, yang lagi-lagi memaksa depelover melakukan kerja extra.

####2.5.3	Custom Dependencies
Seorang developer mungkin perlu menyiapkan sebuah versi custom dari ketergantungan aplikasinya. Beberapa sistem pemaketan bisa mengatasi versi custom dari sebuah dependency, namun yang lainnya tidak bisa dan mengatasi secara berbeda.

`last updated: 9/25/2014 2:21:54 AM `