# BambangShop Publisher App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases and methods to access the databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a basic functionality that makes BambangShop work: ability to create, read, and delete `Product`s.
This repository already contains a functioning `Product` model, repository, service, and controllers that you can try right away.

As this is an Observer Design Pattern tutorial repository, you need to implement another feature: `Notification`.
This feature will notify creation, promotion, and deletion of a product, to external subscribers that are interested of a certain product type.
The subscribers are another Rocket instances, so the notification will be sent using HTTP POST request to each subscriber's `receive notification` address.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Publisher" folder.
This Postman collection also contains endpoints that you need to implement later on (the `Notification` feature).

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    APP_INSTANCE_ROOT_URL="http://localhost:8000"
    ```
    Here are the details of each environment variable:
    | variable              | type   | description                                                |
    |-----------------------|--------|------------------------------------------------------------|
    | APP_INSTANCE_ROOT_URL | string | URL address where this publisher instance can be accessed. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)

## Mandatory Checklists (Publisher)
-   [ ] Clone https://gitlab.com/ichlaffterlalu/bambangshop to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [ ] Commit: `Create Subscriber model struct.`
    -   [ ] Commit: `Create Notification model struct.`
    -   [ ] Commit: `Create Subscriber database and Subscriber repository struct skeleton.`
    -   [ ] Commit: `Implement add function in Subscriber repository.`
    -   [ ] Commit: `Implement list_all function in Subscriber repository.`
    -   [ ] Commit: `Implement delete function in Subscriber repository.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-1" questions in this README.
-   **STAGE 2: Implement services and controllers**
    -   [ ] Commit: `Create Notification service struct skeleton.`
    -   [ ] Commit: `Implement subscribe function in Notification service.`
    -   [ ] Commit: `Implement subscribe function in Notification controller.`
    -   [ ] Commit: `Implement unsubscribe function in Notification service.`
    -   [ ] Commit: `Implement unsubscribe function in Notification controller.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-2" questions in this README.
-   **STAGE 3: Implement notification mechanism**
    -   [ ] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [ ] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [ ] Commit: `Implement publish function in Program service and Program controller.`
    -   [ ] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1
1. Dalam pola Observer, kebutuhan terhadap antarmuka atau trait bergantung pada kompleksitas struktur observer. Jika observer terdiri dari banyak jenis dan kelas, maka trait dibutuhkan untuk memfasilitasi implementasinya. Namun, dalam kasus BambangShop di mana hanya ada satu kelas Observer, yaitu Subscriber, tidak perlu adanya trait. Dalam hal ini, cukup menggunakan satu struktur model untuk menangani observasi perubahan. Jadi, dalam konteks BambangShop, sebuah Model struct tunggal sudah mencukupi tanpa perlu memperkenalkan antarmuka tambahan.

2. Kita memerlukan DashMap untuk efisiensi pemetaan antara produk dan subscriber. Jika menggunakan Vec, perlu membuat dua Vec terpisah untuk setiap produk, yang bisa mempersulit pengelolaan data. DashMap memudahkan akses dan pemeliharaan data dengan pemetaan langsung antara produk dan subscriber.

3. Dalam pemrograman Rust, kepatuhan yang ketat dari kompiler memastikan program thread-safe. Pada kasus variabel statis Daftar Pelanggan (SUBSCRIBERS), DashMap digunakan untuk memastikan keamanan penggunaan HashMap oleh thread. Pertimbangkan apakah DashMap masih diperlukan atau pola Singleton dapat digunakan sebagai alternatif.

#### Reflection Publisher-2
1. Dalam pola MVC, di mana Model mencakup penyimpanan data dan logika bisnis, pemisahan antara "Service" dan "Repository" diperlukan untuk mematuhi prinsip tanggung jawab tunggal. Ini memungkinkan isolasi tanggung jawab yang berbeda, dengan "Service" menangani logika aplikasi dan "Repository" mengelola akses data. Pemisahan ini meningkatkan modularitas dan mempermudah pengembangan dan pemeliharaan kode.

2. Jika hanya menggunakan Model tanpa lapisan lain, program akan memiliki keterikatan yang tinggi. Ini berarti jika terjadi perubahan, banyak penyesuaian yang harus dilakukan dalam kode. Intinya, penggunaan Model tanpa lapisan lain akan meningkatkan kompleksitas kode karena ketergantungan erat antara mereka, menyebabkan perubahan dalam satu dapat berdampak luas pada yang lain.

3. Saya telah memperdalam pemahaman saya tentang Postman, alat yang sangat membantu dalam menguji aplikasi yang dibuat. Dengan Postman, saya dapat memastikan bahwa respons aplikasi sesuai dengan harapan berdasarkan permintaan yang saya buat. Saya juga dapat menyesuaikan metode yang diperlukan, seperti CRUD, untuk memverifikasi keakuratan data. Beberapa fitur yang saya temukan berguna termasuk kemampuan untuk mengatur dan menyimpan koleksi permintaan HTTP, mengotomatisasi pengujian dengan skrip, serta menyediakan lingkungan yang terisolasi untuk menguji integrasi dengan API eksternal. Saya juga mengapresiasi fitur pengujian otomatis yang memungkinkan saya untuk menjalankan serangkaian tes secara berkala untuk memastikan konsistensi dan kualitas aplikasi.

#### Reflection Publisher-3
