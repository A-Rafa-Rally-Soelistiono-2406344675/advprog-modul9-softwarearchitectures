# Understanding Subscriber and Message Broker

What is AMQP?

Menurut saya, AMQP atau Advanced Message Queuing Protocol adalah protokol komunikasi yang digunakan agar aplikasi dapat saling mengirim dan menerima pesan melalui message broker. Dalam konteks tutorial ini, saya menggunakan AMQP sebagai aturan komunikasi antara publisher, subscriber, dan RabbitMQ, sehingga pesan tidak dikirim langsung dari satu program ke program lain, tetapi lewat perantara broker yang mengatur antrean pesan.

What does it mean? `guest:guest@localhost:5672`, what is the first `guest`, what is the second `guest`, and what is `localhost:5672` for?

Menurut saya, bagian `guest:guest@localhost:5672` adalah informasi koneksi yang dipakai aplikasi untuk terhubung ke RabbitMQ. `guest` yang pertama adalah username untuk login ke RabbitMQ, sedangkan `guest` yang kedua adalah password dari username tersebut. `localhost:5672` berarti aplikasi saya mencoba terhubung ke RabbitMQ yang berjalan di komputer lokal saya sendiri, dengan port `5672` sebagai port default yang digunakan oleh AMQP untuk komunikasi dengan message broker.

# Understanding Publisher and Message Broker

How much data your publisher program will send to the message broker in one run?

Menurut saya, program publisher saya akan mengirim lima data atau lima pesan ke message broker dalam satu kali run. Hal ini terlihat dari lima pemanggilan `publish_event` di dalam fungsi `main`, dengan masing-masing pesan berisi `user_id` dan `user_name` yang berbeda, yaitu data untuk Amir, Budi, Cica, Dira, dan Emir.

The url of: `amqp://guest:guest@localhost:5672` is the same as in the subscriber program, what does it mean?

Menurut saya, URL `amqp://guest:guest@localhost:5672` yang sama pada publisher dan subscriber berarti kedua program tersebut terhubung ke message broker yang sama, yaitu RabbitMQ di komputer lokal saya. Publisher memakai URL ini untuk mengirim pesan ke broker, sedangkan subscriber memakai URL yang sama untuk mendengarkan dan menerima pesan dari broker tersebut, sehingga keduanya dapat berkomunikasi melalui queue yang sama.

# Running RabbitMQ as Message Broker

Saya menjalankan RabbitMQ menggunakan Docker dengan image `rabbitmq:3.13-management`, lalu membuka management UI melalui `http://localhost:15672` dan login menggunakan username `guest` serta password `guest`. Screenshot berikut menunjukkan RabbitMQ sudah berjalan sebagai message broker di komputer lokal saya.

![RabbitMQ running as message broker](tutorial8/publisher/images/rabbitmq-running.png)

# Sending and Processing Event

Saya menjalankan subscriber terlebih dahulu agar program siap menerima event dari message broker. Setelah itu saya menjalankan publisher, dan publisher mengirim lima event `UserCreatedEventMessage` ke RabbitMQ. Event tersebut kemudian diterima dan diproses oleh subscriber, terlihat dari terminal subscriber yang menampilkan lima pesan masuk dengan `user_id` dan `user_name` berbeda.

![Publisher and subscriber terminal output](tutorial8/publisher/images/publisher-subscriber.png)

Pada dashboard RabbitMQ, terlihat ada koneksi, channel, queue, dan consumer yang aktif ketika subscriber dan publisher berkomunikasi melalui message broker. Hal ini menunjukkan bahwa RabbitMQ berhasil menjadi perantara antara publisher yang mengirim event dan subscriber yang menerima event.

![RabbitMQ while sending and processing event](tutorial8/publisher/images/rabbitmq-running-event.png)
