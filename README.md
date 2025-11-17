# UTS_245410077_REDITYA-NUR-KAROMAH

#JAWABAN UTS
#1. Jelaskan teorema CAP dan BASE dan keterkaitan keduanya. Jelaskan menggunakan contoh yang pernah anda gunakan. 

a. Teorema CAP menjelaskan bahwa dalam sistem terdistribusi, sebuah sistem tidak dapat sekaligus memenuhi Consistency,
   Availability, dan Partition Tolerance secara bersamaan. Artinya, ketika terjadi gangguan jaringan antar-node, sistem 
   harus memilih apakah ingin tetap konsisten atau tetap tersedia. Sistem yang memprioritaskan konsistensi akan memastikan 
   semua node memiliki data yang sama meskipun harus menolak beberapa permintaan, sedangkan sistem yang mengutamakan ketersediaan
   tetap merespons permintaan meskipun data yang diberikan belum tentu versi terbaru. Konsep CAP ini kemudian berkaitan dengan 
   pendekatan BASE yang banyak digunakan oleh database NoSQL.

b. Sementara BASE itu lebih ke pendekatan praktis yang sering dipakai ketika kita memilih ketersediaan 
   lebih tinggi. Sistem yang saya pakai tadi akhirnya condong ke konsep BASE—server tetap melayani (basically available),
   datanya kadang terlihat belum sinkron (soft state), lalu beberapa detik kemudian baru menyamakan diri setelah replikasi 
   berjalan (eventual consistency). Jadi, hubungan CAP dan BASE itu seperti teori dan praktik: CAP memberi batasan bahwa 
   kita tidak bisa punya semuanya ketika jaringan bermasalah, sedangkan BASE adalah cara membangun sistem yang tetap 
   “berjalan lancar” walaupun konsistensi sempurna baru tercapai beberapa saat kemudian.

c. contohnya 
   saya memakai dua aplikasi catatan di HP dan laptop yang tersinkron lewat internet. Pernah beberapa kali saya memperbarui catatan 
   di HP ketika jaringan sedang jelek. Aplikasi tetap bisa dipakai (availability), tapi perubahan di HP tidak langsung muncul di laptop 
   (consistency hilang karena “partition”, yaitu koneksi terputus). Setelah koneksi pulih, catatan di laptop akhirnya ikut berubah. Situasi 
   ini menggambarkan konsep BASE, yaitu konsistensi yang datang belakangan, dan sekaligus menunjukkan bagaimana CAP bekerja: sistem memilih tetap tersedia meskipun
   konsistensi sementara hilang. Dari pengalaman itu, terlihat jelas bahwa CAP dan BASE saling berkaitan—ketika sistem memilih tetap 
   berjalan meskipun terjadi gangguan jaringan, maka otomatis sistem menerapkan prinsip BASE sebagai cara menjaga pengalaman pengguna tetap lancar.


#2. Jelaskan keterkaitan antara GraphQL dengan komunikasi antar proses pada sistem terdistribusi. Buat diagramnya. 
GraphQL dapat berperan sebagai penghubung komunikasi antar proses dalam sebuah sistem terdistribusi karena ia bertindak 
sebagai pintu masuk tunggal yang menerima permintaan dari klien dan meneruskannya ke layanan-layanan lain di belakangnya.
Dalam sistem yang terdiri dari banyak microservice, setiap layanan biasanya memiliki fungsi dan data sendiri-sendiri, sehingga
klien perlu berkomunikasi dengan beberapa layanan sekaligus. Jika menggunakan REST biasa, klien harus memanggil banyak endpoint 
yang berbeda, sedangkan dengan GraphQL, klien cukup mengirim satu query dan GraphQL akan menyalurkannya ke layanan yang relevan.
Proses seperti ini membuat komunikasi antar proses di backend menjadi lebih teratur karena semua panggilan dari klien hanya melewati 
satu titik koordinasi. GraphQL kemudian meneruskan permintaan itu ke service lain seperti Auth, User, Post, atau Comment sesuai bagian 
data yang diminta klien. Dari situ terlihat bahwa GraphQL bukan hanya alat query data, tetapi juga menjadi jembatan komunikasi antar proses
dalam sistem terdistribusi yang terdiri dari banyak microservice.
