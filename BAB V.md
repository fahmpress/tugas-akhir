##BAB V - KESIMPULAN DAN SARAN
###5.1 Kesimpulan
1.	Union File System yang menjadi *backend* sistem penyimpanan container Docker terbukti membuat proses *deployment* container Docker menjadi sangat efektif jika dibandingkan dengan mesin virtual tradisional seperti VirtualBox. Hasil pengujian menunjukan penggunaan penyimpanan VirtualBox setelah dialakukan 2 proses snapshot adalah 717.36 MB, sedangkan Docker hanya menggunakan 96.26 MB dengan 2 proses snapshot yang sama.

2.	Hasil pengujian menunjukan adanya perbedaan yang signifikan pada penggunaan memory antara Docker dan virtual mesin tradisional. 5 mesin virtual yang dijalankan VirtualBox mengkonsumsi memory sebesar 1.18 GB, sedangkan 10 container Docker yang dijalankan hanya mengkonsumsi memory sebesar 27 MB. Hal ini membuktikan bahwa Docker engine menjalankan container dengan isolasi pada level proses hingga menjadikan container sangat ringan jika dibandingkan dengan virtual mesin tradisional, dan hampir tidak menambah *overhead* pada mesin host.
 
3.	Kompabilitas container Docker pada Ubuntu dan CentOS membuktikan bahwa Docker merupakan software yang lintas platform. Hal ini menjadikan *Dockerized web application* fleksibel dan bisa didistribusikan ke berbagai host yang berbeda sistem operasi. 

4.	Pengujian yang dilakukan dengan menjalankan *dockerized web app* yang sama pada Laptop dengan sistem operasi berbasis grafis dan pada mesin virtual dengan sistem oparsi berbasis text, membuktikan container Docker cukup flexible untuk dijalankan di berbagai *environment* host yang berbeda.
	
5.	Deployment aplikasi berbasis web dengan Docker akan mengurangi tingkat kecemasan para *developer* akan *source code* yang mereka kembangkan di dalam container, bahwa proses *dockerizing* aplikasi dengan container Docker dapat menangani permasalahan ketergantungan aplikasi seperti *conflicting dependencies*.

###5.2 Saran
Melihat banyaknya keuntungan yang bisa didapat dari Docker, penulis menyarankan kepada para developer aplikasi web pada umumnya dan khususnya mahasiswa politeknik agar dapat memanfaatkan Docker sebagai standar tool dalam pengembangan aplikasi berbasis web.