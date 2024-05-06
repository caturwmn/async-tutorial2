# async-tutorial2
1. Original code
![Screenshot hasil awal](screenshot/result_1.png)
Untuk dapat menjalankan server dan client secara terpisah, kita harus membuat mereka menjadi binary yang berbeda di cargo.toml lalu kita buka project melalui beberapa cli sekaligus dan memulai satu sebagai server dan 3 sebagai client (dengan cargo run --bin nama-bin). Ketika kita mengetik beberapa hal di client dan mengetik enter, pesan dari client akan terkirim ke server dan server mengirimkan pesan tersebut ke semua client. Lalu ketika client mendapat update dari server, client akan mencetak "from server: " lalu pesan yang diterima dari server.

2. Modify 
![Screenshot setelah di ganti](screenshot/result_2.png)
Hal yang harus diganti agar program bisa berjalan seperti seharusnya adalah memodifikasi port yang dibind oleh TCPListener menjadi 8080 di fungsi main server.rs. Dapat dilihat bahwa socket yang digunakan oleh server bukanlah webserver melainkan TCP Socket dan listener yang digunakan akan menunggu koneksi apapun yang dilakukan ke uri yang dibind yaitu localhost:8080 dan mengaccept koneksi secara otomatis. Pendefinisian dari penggunaan TCP pada server dilakukan dengan menggunakan modul TCPListener yang disediakan oleh rust dari tokio.

3. add IP and port
![Screenshot setelah ditambah ip dan port](screenshot/result_3.png)
Hal yang saya ubah adalah bagian yang berada di dalam fungsi handle connection pada server. Dapat dilihat di dalam loopnya, ketika server mendapat sebuah pesan, server akan mengeprint addres asal pesan tersebut dan mengirimnya kembali ke semu client. Di bawah fungsi yang mengeprint address dan pesan dari client, terdapat fungsi yang langsung mengirim pesan ke semua client yaitu bcast_tx.send(text.into())?. Yang saya ubah adalah saya menambahkan address yang diubah menjadi string (serta ": " agar rapi) ke dalam fungsi send tersebut sehingga client bisa mendapat address dari client lainnya (ip dan port).