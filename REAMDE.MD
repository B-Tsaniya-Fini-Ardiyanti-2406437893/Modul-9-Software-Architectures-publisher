# RabbitMQ Publisher & Subscriber Explanation

## a. How much data will the publisher send to the message broker in one run?

Publisher mengirim 5 pesan dalam satu kali jalan (satu run). Ini terlihat dari kode yang memanggil `publish` sebanyak 5 kali seperti:

```
"user_id": "1", "user_name": "2406...-Amir"
"user_id": "2", "user_name": "2406...-Budi"
"user_id": "3", "user_name": "2406...-Cica"
"user_id": "4", "user_name": "2406...-Dira"
"user_id": "5", "user_name": "2406...-Emir"
```

Jadi dalam satu run, publisher mengirim **5 pesan** ke message broker.

---

## b. The URL `amqp://guest:guest@localhost:5672` is the same in both publisher and subscriber — what does it mean?

Artinya publisher dan subscriber terhubung ke message broker yang sama, yaitu RabbitMQ yang berjalan di `localhost:5672` dengan kredensial yang sama (`guest:guest`).

- **Publisher** menulis/mengirim pesan **ke** broker tersebut
- **Subscriber** membaca/menerima pesan **dari** broker yang sama

## RabbitMQ Running Screenshot

![Running RabbitMQ](assets/rabbitmq-screenshot.png)

## Sending and Processing Event

![Sending and Processing Event](assets/sending-processing.png)

Saat publisher di run, publisher mengirim 5 events ke RabbitMQ message broker. 
Subscriber yang terhubung ke broker yang sama melalui `amqp://guest:guest@127.0.0.1:5672`,
menerima dan memproses setiap event satu per satu. Publisher bertindak seperti event producer, 
sementara subscriber bertindak sebagai event consumer.

## Monitoring Chart Based on Publisher

![RabbitMQ Monitoring](assets/rabbitmq-chart.png)

The spikes on the message rates chart correspond to each time the publisher 
was run (`cargo run`). Every time the publisher runs, it sends 5 events at once 
to the message broker, causing a sudden spike in the publish rate. 
After all 5 messages are delivered and consumed by the subscriber, 
the rate drops back to 0. This shows how the message broker acts as 
a middleman between publisher and subscriber.

## Monitoring Chart Based on Publisher

![RabbitMQ Monitoring](assets/rabbitmq-chart.png)

Lonjakan (spikes) pada grafik message rates muncul setiap kali program publisher dijalankan (`cargo run`). 
Tiap kali publisher jalan, publisher langsung mengirim 5 event sekaligus ke message broker, maka dari itu publish rate-nya langsung melonjak tajam. Lalu, begitu ke-5 pesannya selesai dikirim dan diterima oleh subscriber, grafiknya akan turun lagi ke angka 0. Hal ini menunjukan bagaimana peran message broker yang benar-benar bekerja sebagai perantara (middleman) antara publisher dan subscriber.

