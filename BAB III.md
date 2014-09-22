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

2. Uji Efektifitas dengan Studi Komparasi

Sesuai paparan di atas terlihat perbedaan penggunaan penyimpanan Docker dengan mesin virtual tradisional. Dalam hal ini penulis akan melakukan pembuktian hipotesa tersebut dengan melakukan komparasi antara Docker dan VirtualBox, sehingga terlihat efektifitas Docker dibandingkan mesin virtual tradisional.

Untuk malakukan pengujian tersebut penulis akan menginstall Docker dan VirtualBox pada mesin host dan sistem operasi yang sama secara bergantian agar hardware yang digunakan identik dan sama persis, hal ini dilakukan atas pertimbangan integritas pengujian. Lalu menjalankan satu mesin virtual (container) dan melakukan 2 proses yang masing-masing proses akan diambil snapshot-nya. Parameter uji yang digunakan dalam pengujian ini adalah besaran penggunaan penyimpanan (*storage*)

#####3.1.1.2.	Penghematan Memory
Dalam proses deployment-nya Docker container menggunakan shared kernel dari mesin host tanpa ada perantara lapisan virtualisasi seperti *hypervisor*, maka proses menjadi lebih ringan sehingga bisa menghemat memory dan overhead pada mesin host (*zero overhead*) sehingga memungkinkan untuk menjalankan banyak container dalam satu mesin, berbeda dengan virtualisasi tradisional yang menggunakan *hypervisor* dan kernel tersendiri dari mesin host.

![alt text](https://github.com/fahmpress/tugas-akhir/blob/master/images/gambar3.2.jpg "Gambar 3.2")

Gambar 3.2 Shared Host Kernel pada Docker

Untuk pengujian ini akan dilakukan komparasi saat proses *deployment* mesin virtual (container) antara Docker dan VirtualBox. Docker dan Virtualbox akan diinstal pada mesin host dan sistem operasi yang sama. Setelah itu akan dijalankan beberapa mesin virtual dan container lalu akan dilihat penggunaan memorynya. Pengukuran memory akan menggunakan htop. Parameter uji dalam pengujian ini adalah besaran kenaikan memory yang digunakan saat menjalankan mesin virtual atau container.

####3.1.2	Uji Kompabilitas Docker Terhadap Perbedaan Versi Aplikasi, Platform dan Hardware (Environment)

Dalam pengembangan sebuah aplikasi berbasis web, environment tempat dimana aplikasi tersebut di-hosting akan menjadi masalah jika tidak sesuai dengan tempat aplikasi dikembangkan atau permasalahan pada software dependencies-nya. Bentuk permasalahan ini bisa bermacam-macam khususnya dalam sistem operasi linux, seperti; Many dependencies, long cains of dependencies, cross-platform dependencies dan conflicting dependencies. Aplikasi yang dibangun dengan banyak dukungan dependencies akan sulit untuk dijalankan pada environment yang berbeda, karena untuk menjalankan aplikasi tersebut akan dilakukan proses re-packaging dependencies-nya. Docker akan menjawab permasalahan pada proses pengembangan aplikasi web dengan metode tradisional tersebut, dan Docker menjadikan aplikasi yang dibangun menjadi portable. 

Contoh kasus adalah perbedaan environment pada developer, testing dan hosting aplikasi. Aplikasi yang dikembangkan harus mampu dijalankan di environment apapun di internet atau lokal, untuk melakukan itu, sysadmin harus menyiapkan environment dengan melakukan re-packaging dependencies untuk membuat aplikasi bisa berjalan, dan hal tentu saja bermasalah jika dependencies yang dibutuhkan oleh sebuah aplikasi sangat banyak. Contoh kasus lain semisal aplikasi web PHP yang berbeda versi dengan server PHP pada server, jika versi server PHP berbeda dengan versi aplikasi yang akan di-hosting, maka aplikasi harus upgrade versinya karena masalah kompabilitas. Pengujian ini dilakukan untuk membuktikan bahwa Docker bisa menjawab permasalahan ketergantungan terhadap dukungan versi aplikasi.
 
Docker mengklaim sekali developer membangun sebuah aplikasi maka Dockerized Apps hampir bisa dijalankan dimanapun, termasuk hardware server dan platform. Kompablitas pada lingkungan hardware sudah diuji coba pada point sebelumnya dengan menjalankan dockerized app pada PC dan Laptop. Untuk uji coba pada perbedaan platform akan dilakukan pada 2 mesin virtual yang berbeda sistem operasi. Dalam hal ini penulis menggunakan Ubuntu dan CentOS.
Untuk variasi uji ini akan dibagi menjadi dua metode uji :

1.	Pengujian Cross-platform Dependencies, Penulis akan membuat sebuah Dockerized apps pada mesin Ubuntu, lalu aplikasi yang telah dibangun tersebut akan dijalankan pada mesin CentOS tanpa merubah apapun pada aplikasinya.
2.	Pengujian Conflicting Dependencies, dengan menjalankan versi aplikasi yang berbeda pada mesin (server) yang sama. aplikasi yang akan digunakan untuk uji coba adalah PHP versi 4 dan 5 yang dipaketkan sebagai LAMP server.
3.	Pengujian Many Dependencies, dengan menjalankan aplikasi yang telah dibuat pada PC akan diuji kompabilitasnya pada mesin (hardware) lain yang memiliki environment berbeda, dalam hal ini penulis menggunakan laptop tanpa harus melakukan pemaketan dependency atau konfigurasi lain.

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
