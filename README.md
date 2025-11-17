# UTS_245410077_REDITYA-NUR-KAROMAH

#JAWABAN UTS
#1. Jelaskan teorema CAP dan BASE dan keterkaitan keduanya. Jelaskan menggunakan contoh yang pernah anda gunakan. 
Penjelasan singkat
CAP (Brewer): pada sistem terdistribusi ada tiga sifat penting: Consistency (C), Availability (A), dan Partition tolerance (P). Teorema CAP menyatakan: ketika terjadi network partition (node tidak bisa saling berkomunikasi), sistem hanya bisa menjamin C atau A, bukan keduanya. Karena partisi jaringan nyata bisa terjadi kapan saja, praktiknya sistem harus menerima P dan memilih antara C atau A saat partisi.
BASE adalah pola desain untuk sistem yang memilih Availability saat terjadi partisi. Singkatan:
Basically Available — sistem tetap merespons request.
Soft state — state dapat berubah-ubah sebelum konvergen.
Eventual consistency — pada akhirnya semua replica akan konvergen kalau tidak ada update lebih lanjut.
Hubungan CAP ↔ BASE
CAP adalah aturan trade-off (teori).
BASE adalah pendekatan praktis bila kita memilih A + P dari CAP: sistem tetap melayani, lalu menyelesaikan inkonsistensi nanti sampai konvergen.
Contoh nyata (yang saya pernah pakai — shopping cart terdistribusi)
Kasus: layanan shopping cart yang disebar ke beberapa region supaya akses cepat.
Arsitektur: setiap region punya replica cart lokal yang melayani pengguna regional.
Kejadian: kalau ada network partition antara region A dan central service, user di region A masih bisa add-to-cart (system memilih Availability). Operasi dicatat sebagai event lokal (soft state).
Setelah koneksi pulih, event direplikasi ke central, dan konflik (mis. duplicate item) diselesaikan sesuai kebijakan (mis. jumlah ditambah atau last-writer-wins).
Hasil: pengguna jarang menemui kegagalan operasional, dan data akan mencapai konsistensi akhirnya — eventual consistency.

#2. Jelaskan keterkaitan antara GraphQL dengan komunikasi antar proses pada sistem terdistribusi. Buat diagramnya. 
Inti hubungan (sederhana)
GraphQL adalah bahasa query untuk API — berguna untuk meminta bentuk data yang pas.
Di arsitektur microservices, GraphQL biasanya ditempatkan di API Gateway atau BFF (Backend-for-Frontend). Di sana GraphQL mengorkestrasi banyak panggilan antar-layanan (IPC) — mis. HTTP, gRPC, atau via message queue — lalu menggabungkan hasilnya menjadi satu response untuk klien.
Jadi GraphQL bukan protokol IPC; dia adalah lapisan komposisi yang menerjemahkan query klien menjadi banyak panggilan IPC internal.
Kapan GraphQL berguna
Klien cuma butuh satu request untuk gabungan data dari beberapa layanan → mengurangi round-trip.
Menyembunyikan kompleksitas backend yang terdistribusi.
Cocok ketika data yang diminta bersifat read/aggregate; untuk operasi write/transactional biasanya tetap pakai endpoint tersendiri.
