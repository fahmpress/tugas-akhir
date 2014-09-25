##BAB IV - IMPLEMENTASI DAN PENGUJIAN

###4.1  Uji Efektifitas Docker 
####4.1.1   Instalasi Virtualbox dan Docker

Sistem operasi yang digunakan untuk pengujian ini adalah Ubuntu 14.04 LTS Server. Install VirtualBox via terminal dengan menggunakan perintah:
    
    apt-get install virtualbox
atau mendownload pada halaman resmi virtualbox dan menginstallnya secara manual. Dalam hal ini penulis mendownload virtualbox dan menginstalnya secara manual, untuk mendapatkan virtualbox dengan versi terakhir. Setelah download selesai, install virtualbox dengan perintah `dpkg -i /direktori/installer.deb`:

    dpkg -i /Downloads/virtualbox-4.3_4.3.16-95972~Ubuntu~raring_amd64.deb

Setelah instalasi virtualbox selesai, buat virtual mesin dengan mengklik `new` pada menu lalu beri nama dan pilih sistem operasi yang akan diinstall.

Gambar 4.2 Membuat mesin virtual baru

Langkah selanjutnya menentukan besaran memory yang akan digunakan oleh mesin virtual. Dalam hal ini penulis menggunakan memory sebesar 256 MB. Sumber daya diambil sekecil mungkin untuk meminimalkan *overhead* pada mesin host.

Gambar 4.3 Menentukan besaran memory

