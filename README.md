# Understanding Subscriber and Message Broker

What is AMQP?

Menurut saya, AMQP atau Advanced Message Queuing Protocol adalah protokol komunikasi yang digunakan agar aplikasi dapat saling mengirim dan menerima pesan melalui message broker. Dalam konteks tutorial ini, saya menggunakan AMQP sebagai aturan komunikasi antara publisher, subscriber, dan RabbitMQ, sehingga pesan tidak dikirim langsung dari satu program ke program lain, tetapi lewat perantara broker yang mengatur antrean pesan.

What does it mean? `guest:guest@localhost:5672`, what is the first `guest`, what is the second `guest`, and what is `localhost:5672` for?

Menurut saya, bagian `guest:guest@localhost:5672` adalah informasi koneksi yang dipakai aplikasi untuk terhubung ke RabbitMQ. `guest` yang pertama adalah username untuk login ke RabbitMQ, sedangkan `guest` yang kedua adalah password dari username tersebut. `localhost:5672` berarti aplikasi saya mencoba terhubung ke RabbitMQ yang berjalan di komputer lokal saya sendiri, dengan port `5672` sebagai port default yang digunakan oleh AMQP untuk komunikasi dengan message broker.
