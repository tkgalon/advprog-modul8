# advprog-modul8

Nama: Muhammad Zaid Ats Tsabit <br>
NPM: 2306224410 <br>
Kelas: Advprog-B
<hr>

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

Pada Unary RPC, komunikasi terhadi 1-on-1, dimana client mengirim satu permintaan dan server mengembalikan satu respons. Hal tersebut cocok untuk operasi sederhana seperti login atau pengambilan satu data. Lalu, server streaming digunakan ketika server mengirimkan beberapa respons atas satu permintaan, seperti menampilkan riwayat transaksi. Sedangkan, bi-directional streaming memungkinkan client dan server saling mengirimkan stream data secara bersamaan, cocok untuk aplikasi real-time seperti chat.

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

Untuk autentikasi, strategi umum yang bisa digunakan adalah menggunakan token, seperti JWT (JSON Web Token), untuk memverifikasi identitas client. Server akan memeriksa validitas token sebelum memproses permintaan. Lalu, untuk otorisasi, pendekatan Role-Based Access Control (RBAC) dapat digunakan, di mana setiap pengguna memiliki role tertentu dan hanya dapat mengakses endpoint yang sesuai dengan hak aksesnya. Sedangkan untuk enkripsi data, gRPC secara default mendukung komunikasi aman dengan TLS (Transport Layer Security), yang menjamin bahwa data terenkripsi selama transmisi antar client dan server. Selain itu, validasi input dan sanitasi data juga mungkin bisa dipertimbangkan.

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

Menangani bi-directional streaming di Rust cukup "rumit" karena kita harus mengelola dua alur komunikasi asynchronous secara bersamaan. Pada aplikasi chat, potensi masalah mencakup deadlock, message loss jika channel tertutup, dan sulitnya mengelola state client secara bersamaan.

4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?

ReceiverStream mempermudah konversi dari channel biasa menjadi stream yang bisa digunakan langsung oleh gRPC server. Ini membuat proses pengiriman data yang berkelanjutan (seperti list transaksi) menjadi nudah dibaca. Namun, kelemahannya muncul jika jumlah data yang dikirim sangat besar atau jika pengelolaan channel tidak optimal. Risiko bottleneck atau kehilangan message bisa terjadi jika channel penuh atau receiver tidak cepat mengonsumsi data.

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

Untuk meningkatkan modularitas dan kemudahan pengelolaan kode gRPC di Rust, struktur proyek sebaiknya dipisahkan berdasarkan tanggung jawab. Misalnya, logic dari tiap service (seperti Payment, Transaction, dan Chat) ditempatkan dalam modul atau file terpisah. Dengan demikian, kode menjadi lebih terorganisir dan mudah diuji secara individual. Lalu, menggunakan trait juga membantu dalam membuat kontrak service yang bisa digantikan oleh implementasi lain, yang sangat berguna untuk testing dan refactoring. Prinsip DRY (Don't Repeat Yourself) harus dijaga agar setiap fungsi memiliki satu tanggung jawab yang jelas atau kita bisa implementasi prinsip yang sudah dipelajari seperti SOLID.

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

Untuk menangani kasus yang lebih kompleks, langkah lanjutan perlu ditambahkan seperti validasi input dari user, pengecekan saldo secara real-time, error handling, serta logging transaksi ke dalam database. Selain itu, jika transaksi melibatkan sistem eksternal seperti gateway pembayaran, perlu ada retry mechanism dan rollback system untuk menjaga integritas data jika terjadi kegagalan proses di tengah jalan.

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

Adopsi gRPC sebagai protokol komunikasi membuat perubahan yg signifikan pada desain sistem terdistribusi. Karena gRPC menggunakan .proto sebagai schema standar, yang mana membuat komunikasi antar layanan menjadi lebih konsisten dan tidak tergantung pada bahasa pemrograman tertentu. Ini memungkinkan microservices yang ditulis dalam bahasa berbeda tetap bisa berkomunikasi tanpa hambatan. Dengan HTTP/2 dan Protobuf, efisiensi komunikasi meningkat drastis dibanding REST dan arsitektur menjadi lebih terstruktur dan maintainable.

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

Penggunaan HTTP/2 gRPC memiliki banyak keunggulan dibanding HTTP/1.1. Dengan fitur seperti multiplexing, header compression, dan support full-duplex communication, HTTP/2 jauh lebih efisien dan responsif. Ini membuatnya cocok untuk use case yang butuh performa tinggi seperti streaming data atau komunikasi real-time. Namun, kekurangannya adalah kompleksitas setup dan debuggingnya yang sedikit lebih tinggi, serta belum semua environment mendukung HTTP/2 sebaik HTTP/1.1.

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

REST API bekerja dengan model request-response tradisional, dimana client mengirim satu permintaan dan menunggu satu respons dari server. Ini cukup untuk aplikasi yang bersifat statis atau tidak perlu komunikasi berkelanjutan. Sebaliknya, gRPC mendukung streaming dua arah yang memungkinkan client dan server saling mengirimkan data secara bersamaan. Hal ini memberikan keuggulan dalam aplikasi real-time seperti chat, live monitoring, atau sistem notifikasi, dimana responsivitas dan keberlanjutan pada komunikasi sangat penting.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

Pendekatan schema-based yang digunakan oleh gRPC melalui Protocol Buffers memberikan kejelasan struktur dan efisiensi ukuran data karena semua message harus mengikuti definisi .proto, maka kemungkinan error karena struktur data yang tidak konsisten bisa dikurangi. Ini juga memudahkan validasi dan dokumentasi. Namun, JSON pada REST lebih fleksibel dan lebih cepat untuk didevelop karena tidak memerlukan definisi schema yang kaku.









