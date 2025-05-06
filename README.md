# AdvProg - Module 8

1. **What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?**
- Pada metode Unary, klien mengirim satu permintaan dan menerima satu respons dari server. Pola ini sangat cocok untuk permintaan yang sederhana dan langsung, seperti autentikasi atau mengambil detail pengguna. Sementara itu, metode Server Streaming memungkinkan klien mengirim satu permintaan tetapi menerima banyak respons secara bertahap dari server. Pola ini tepat untuk kasus seperti menampilkan histori transaksi atau notifikasi bertahap, di mana data terus mengalir setelah permintaan awal. Selain itu, terdapat bidirectional streaming, baik klien maupun server dapat saling mengirim dan menerima pesan secara independen dan terus-menerus dalam satu koneksi. Pola ini sangat sesuai untuk aplikasi seperti layanan obrolan (chat) atau pembaruan data real-time, karena mendukung komunikasi dua arah yang aktif.

2. **What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?**
- Untuk autentikasi, sebaiknya menggunakan token seperti JWT atau sertifikat TLS. Otorisasi perlu diterapkan untuk membatasi akses pengguna terhadap resource tertentu. Selain itu, semua komunikasi sebaiknya dienkripsi menggunakan TLS agar data yang dikirim tidak dapat disadap atau dimodifikasi oleh pihak ketiga.

3. **What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?**
- Bidirectional streaming memiliki tantangan seperti sinkronisasi antara stream masuk dan keluar, penanganan error secara asinkron, dan pengelolaan lifecycle koneksi yang kompleks. Dalam aplikasi seperti chat, kesulitan bisa muncul saat menangani koneksi yang tiba-tiba terputus, channel yang penuh, atau penanganan pesan yang datang secara bersamaan dari banyak klien.

4. **What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?**
- Penggunaan tokio_stream::wrappers::ReceiverStream dalam gRPC Rust memberikan kemudahan dalam mengubah channel async menjadi stream yang dapat dikirim ke klien. Keuntungannya adalah integrasi yang sederhana dengan kanal komunikasi antar-task. Namun, kelemahannya terletak pada keterbatasan kinerja ketika menangani jumlah data yang sangat besar atau ketika diperlukan kontrol yang lebih kompleks terhadap aliran data.

5. **In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?**
- Struktur kode sebaiknya dipisah menjadi beberapa modul seperti services, handlers, dan utils. Penggunaan trait untuk mendefinisikan kontrak layanan, serta pembagian logic ke dalam file terpisah, akan memudahkan dalam pengujian dan pengembangan di masa depan. Modularitas ini juga memungkinkan reuse komponen dan meningkatkan skalabilitas aplikasi.

6. **In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?**
- Dalam implementasi MyPaymentService, untuk menangani logika pembayaran yang lebih kompleks, perlu ditambahkan validasi input, pengecekan saldo pengguna, integrasi dengan sistem pembayaran eksternal, dan pencatatan transaksi ke dalam database. Selain itu, perlu ada manajemen error yang baik, retry mechanism untuk transaksi gagal, serta audit log untuk keperluan keamanan dan pelacakan.

7. **What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?**
- Menggunakan gRPC dalam sistem terdistribusi berdampak pada arsitektur yang lebih efisien dan terstruktur. Karena gRPC menggunakan Protobuf, komunikasi antar layanan menjadi lebih cepat dan hemat bandwidth. Selain itu, gRPC mendukung berbagai bahasa pemrograman sehingga meningkatkan interoperabilitas antar layanan yang dibangun dengan teknologi berbeda. Namun, untuk integrasi dengan frontend berbasis web, diperlukan proxy atau gateway karena browser tidak mendukung HTTP/2 secara langsung untuk gRPC.

8. **What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?**
- HTTP/2 yang digunakan oleh gRPC memiliki keunggulan dibanding HTTP/1.1 seperti multiplexing, header compression, dan aliran data yang lebih efisien. Hal ini menjadikan komunikasi lebih cepat dan responsif. Namun, kompleksitas implementasinya lebih tinggi. Sementara WebSocket di atas HTTP/1.1 memungkinkan komunikasi dua arah, tetapi tidak seefisien dan seterstandar gRPC untuk API berbasis RPC.

9. **How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?**
- REST API menggunakan model permintaan-respons satu arah yang cocok untuk komunikasi tradisional, tetapi kurang optimal untuk interaksi real-time. Sebaliknya, gRPC dengan bidirectional streaming memungkinkan pertukaran data dua arah secara simultan, sehingga lebih sesuai untuk aplikasi seperti live chat atau monitoring sistem yang membutuhkan respons instan tanpa polling.

10. **What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?**
- Pendekatan berbasis skema seperti Protocol Buffers di gRPC memberikan struktur data yang lebih kuat dan aman karena validasi dilakukan secara ketat berdasarkan definisi .proto. Ini berbeda dengan JSON dalam REST API yang lebih fleksibel namun rentan kesalahan karena tidak ada skema tetap. Protobuf juga lebih efisien secara ukuran dan kecepatan dibanding JSON yang bersifat lebih verbose dan dinamis.

















