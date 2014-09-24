##BAB I - PENDAHULUAN

###1.1	Latar Belakang Masalah
 
Perusahaan bisnis dan institusi yang mempunyai aplikasi berbasis client-server (web app) saat ini banyak menggunakan layanan cloud computing untuk hosting aplikasinya, terutama aplikasi yang bersifat publik dan diakses secara real time oleh penggunanya. Dengan kata lain sebuah perusahaan atau instansi ini menyewa layanan cloud pada sebuah ISP yang berupa infrastruktur (Data Center) atau platform. Hal yang jadi pertimbangan untuk menggunakan Cloud Computing dibanding komputasi tradisional adalah efektifitas, keamanan, skalabilitas, kolaborasi dan lebih murah.

Karena kemajuan internet dan cloud computing saat ini sangat cepat, pelaku bisnis yang memiliki system informasi jaringan memiliki banyak opsi untuk menanamkan system miliknya; hosting dengan shared directory, hosting dalam sebuah VPS, menyewa Data Center di cloud, atau membangun Data Center local sendiri. Tentu saja hal itu akan di sesuaikan dengan kebutuhan dan budget perusahaan tersebut. Sistem informasi dalam sebuah perusahaan bersifat dinamis sesuai perkembangan bisnisnya, sehingga dibutuhkan sebuah system dengan skalabilitas yang tinggi. Jika sebuah system dikembangkan untuk memenuhi kemajuan sebuah perusahaan maka aplikasi akan melakukan migrasi jika terjadi perubahan pada infrastrukturnya.
Perkembangan yang bersifat dinamis ini menjadi masalah bagi pengembang dan administrator sebuah system aplikasi, terutama aplikasi berbasis web. Pengembang harus mempunyai aplikasi yang mampu berjalan dalam lingkungan yang berbeda untuk menjawab permasalahan seperti saat melakukan depelopment dan testing pada environment yang berbeda atau migrasi server. Kendala yang sering terjadi adalah Conflicting Dependencies, Missing Dependencies dan perbedaan platform server itu sendiri.

Contoh kasus, saat pengembang membuat software di lingkungan virtualisasi, maka saat testing atau dijalankan oleh sysadmin akan dilakukan di lingkungan yang berbeda seperti hardware server atau di cloud. Hal ini menjadi masalah saat aplikasi dan server menggunakan versi software yang berbeda, atau platform yang digunakan oleh server berbeda dengan platform saat software itu di kembangkan (Dependencie Hell). Untuk itu muncul sebuah software PaaS untuk menjawab permasalahan tersebut yaitu Docker.

Docker merupakan software virtualisasi jenis Operating system-level virtualization berbasis LXC (Linux Container) yang memungkinkan developer aplikasi membuat, menguji dan menjalankan aplikasi dalam sebuah lingkungan yang sama, terisolasi dan flexible. Tujuan utama dari virtualisasi ini adalah untuk memudahkan para developer dan sysadmin aplikasi berbasis client-server (Web Application) dalam proses pengembangan, uji coba dan pemaketan kode program dan hosting. Sehingga aplikasi yang dibuat diuji coba dan di jalankan di dalam lingkungan yang berbeda tanpa harus mempertimbangkan dukungan dependencies kembali. Hal itu bisa terjadi karena dengan Docker, seorang pengembang software bisa melakukan pemaketan kode kode program berikut dependencies-nya (stacking code). Oleh karena itu Docker mengklaim, sekali developer membangun aplikasi dengan Docker container maka aplikasi itu bisa dijalankan dimanapun; Laptop, PC, QA Server, Bare Metal dan Cloud selama semua itu menjalankan Docker Engine.
Walaupun Docker software virtualisasi namun berbeda dengan Virtual Mesin tradisional yang menggunakan hypervisor dengan fungsi untuk membuat abstraksi system operasi sehingga kernel host dan guest terpisah, Docker hanya sebuah container yang menggunakan shared kernel dan library dari mesin Host, namun tetap mempunyai lingkungan namespace yang terpisah (terisolasi dari mesin host) seperti PID dan networking.

Docker sangat ringan dan mempunyai mekanisme yang lebih maju jika dibandingkan dengan software virtualisasi lain seperti VirtualBox, indikasinya adalah adanya efektifitas lebih pada Docker dalam  hal penggunaan sumber daya mesin host, karena dalam proses deployment-nya, Docker akan menjalankan sebuah container menggunakan base image dengan metode *file system as a layer*  yang berarti Docker hanya akan menyalin lapisan perubahannya saja untuk dijalankan sebagai duplikasi container yang berbeda dengan base image yang sama, berbeda dengan virtualisasi tradisional dimana kita harus menyalin seluruh container beserta kernel dan library yang berada di dalamnya, hal ini mengakibatkan adanya pengehematan penyimpanan dan memory pada Docker. Kelebihan yang lain adalah docker merupakan software yang berlisensi open source dan juga mempunyai registry publik yang gratis saling berbagi container yang telah kita buat.

Beberapa server farm terbesar di dunia saat ini berdasar teknologi container. Deployment web besar seperti Google dan Twitter, atau penyedia platform seperti Heroku dan dotCloud, semua menjalankan teknologi container, dengan sekala ratusan ribu atau bahkan jutaan container yang berjalan secara paralel. Pemanfaatan Docker sebagai Platform as a Service bisa mempermudah para depelover software dalam pengembangan systemnya, dan juga memudahkan sysadmin untuk menjalankan aplikasi tersebut dimanapun selama lingkungan yang menjalankan aplikasi tersebut menjalankan Docker engine.

###1.2	Identifikasi atau Perumusan Masalah
 
Berdasarkan pemaparan diatas maka penulis mengidentifikasi beberapa rumusan masalah sebagai berikut: 

1. Bagaimana implementasi pengembangan aplikasi berbasis web menggunakan linux container Docker?
2. Bagaimana efektifitas container Docker dalam penggunaan sumber daya penyimpanan dan memory dibandingkan dengan mesin virtual tradisional?
3. Bagaimana kompabilitas container Docker untuk menjalankan aplikasi yang telah dibangun pada platform yang berbeda sebagai cara untuk mengatasi permasalahan cross-platform dependencies?
4. Bagaimana kompabilitas container Docker untuk menjalankan aplikasi yang telah dibangun pada lingkungan *host* yang berbeda?
5. Bagaimana komplabilitas container Docker untuk menjalankan aplikasi yang berbeda versi dalam satu mesin sebagai cara untuk mengatasi permasalahan conflicting dependencies?

###1.3	Batasan Masalah
 
Setelah menelaah rumusan masalah diatas, maka didapat beberapa batasan masalah diantaranya : 

1.	Instalasi komputer host yang akan digunakan untuk menjalankan Docker engine.
2.	Kemanan web server yang akan dikembangkan dengan Docker.
3.	Uji efektifitas yang berkaitan dengan kebutuhan bandwidth yang dibutuhkan oleh pengguna Docker PaaS saat menggunakan registry public milik Docker. 

###1.4	Tujuan dan Manfaat Penelitian
 
Tujuan dan manfaat penulisan tugas akhir ini adalah :

1.	Melakukan pengujian terhadap kompabilitas Docker sebagai Platform as a Service untuk mengatasi permasalahan “Dependency Hell” yang dihadapi developer web dalam pengembangan dan pendistribusian aplikasinya.
2.	Melakukan pengujian terhadap efektifitas Docker sebagai software virtualisasi modern dalam penggunaan sumber daya penyimpanan dan memory, dan membandingkannya dengan software virtualisasi model lama (tradisional).
3.	Mengenalkan penggunaan Docker sebagai Platform as a Service yang mudah digunakan, ringan dan cepat proses deployment-nya.

###1.5	Metode Penelitian

Dalam tulisan ini penulis menggunakan metode eksperimental dengan menggunakan software virtualisasi dan membuat simulasi yang disesuaikan dengan kasus aslinya. Adapun teknik pengumpulan datanya dilakukan dengan dua unsur pengumpulan data:
1.	Studi Pustaka
Data diperoleh dari tulisan-tulisan dan panduan di internet yang berkaitan dengan masalah yang penulis bahas.
2.	Simulasi 
Dilakukan dengan percobaan pembuatan pemodelan dengan berdasarkan panduan yang berkaitan dengan masalah yang di bahas.


###1.6	Sistimatika Penulisan
 
Sistematika penulisan tugas akhir yang digunakan adalah sebagai berikut :

#####BAB I PENDAHULUAN
Dalam bab ini penulis menjelaskan tentang Latar belakang, identifikasi/perumusan masalah dan batasan masalah, tujuan dan manfaat, metode penulisan dan sistematika penulisan.
#####BAB II LANDASAN TEORI
Dalam bab ini penulis menjelaskan mengenai teori-teori yang berkaitan dengan judul tugas akhir ini.
#####BAB III RANCANGAN PENGUJIAN
Dalam bab ini akan menjelaskan mengenai perancangan serta implementasian  dalam penggunaan Docker sebagai Platform as a Service.
#####BAB IV IMPLEMENTASI DAN PENGUJIAN
Dalam bab ini menjelaskan mengenai pengujian kompabilitas Dockerized App saat dijalankan di lingkungan yang berbeda, dan efektifitas penggunaan sumber daya penyimpanan dan memory dalam proses deployment sebuah aplikasi berbasis web.
#####BAB V KESIMPULAN DAN SARAN
Dalam bab ini akan dibahas mengenai kesimpulan yang merupakan hasil dari implementasi dan saran-saran dari penulis sebagai bahan pertimbangan untuk implementasi Docker sebagai Platform as a Service.

`last edited: 9/24/2014 7:53:01 PM  `
