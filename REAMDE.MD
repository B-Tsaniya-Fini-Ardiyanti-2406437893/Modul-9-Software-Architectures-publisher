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