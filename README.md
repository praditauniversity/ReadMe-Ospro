# READ ME FIRST TO RUN OSPRO APPLICATION
Tutorial untuk menjalankan Ospro pada lokal server

Semua microservice yang berada pada repository untuk aplikasi ospro dapat di jalankan di lokal connection.
Cara menjalankan ospro application
## Tutorial 
Repository pada github untuk aplikasi ospro dibagi menjadi tiga yaitu Backend, Gateway dan Frontend.
- Repository Backend : ms-project,ms-gantt,ms-activity,ms-dailyreport,ms-report,ms-user-management. (Semua yang bernama ms (microservice) itu adalah bagian dari backend.)
- Repository Gateway : gateway
- Repository Frontend : mf-main

Repository yang digunakan untuk menjalankan aplikasi ospro yang saat ini adalah ms-project,ms-gantt,ms-activity,ms-dailyreport,ms-report,ms-user-management,gatewa,dan mf-main
jadi lakukanlah penarikan repository pada repository yang bernama di atas untuk menjalakan aplikasi ospro

Setelah melakukan penarikan pada repository yang sudah disebut lakukan langkah selanjutnya yaitu instalasi docker https://www.docker.com/


## Instalasi Docker
Download docker pada link ini https://www.docker.com/ pilih lah sesuai dengan sistem operasi yang anda gunakan seperti windows atau linux
jika anda menginstal menggunakan windows anda perlu melakukan beberapa langkah lagi untuk dapat menjalankan docker 
pergi menuju microsoft store kemudian cari alpine setelah itu carilah aplikasi yang bernama Alpine WSL kemudian download 
atau lalu ikuti tutorial di bawah ini 
https://www.petanikode.com/docker-install/

## How to Build Docker Image dan Run Docker  
Buka visual studio code lalu buka folder ms-project atau ms lainnya 
Buka terminal pada visual studio code 
lalu pada command prompt tuliskan ```docker compose up --build``` (artinya membuild image docker dan melakukan running pada aplikasi docker).
Untuk melakukan docker berjalan pada background application lakukan ```docker compose up --build -d``` (artinya mem-build docker image dan melakukan running pada aplikasi docker dilakukan pada background aplikasi).
Untuk mematikan docker yang sedang berjalan lakukan ```docker compose down```. 
Untuk menghilangkan seluruh data aplikasi beserta database di docker lakukan ```docker compose down -v```. 
Lakukan setiap hal ini pada semua microservice, gateway, frontend yang ingin di jalankan

## Golang Tutorial
Dalam setiap repositori proyek, diimplementasikan Clean Architecture yaitu merupakan pola desain perangkat lunak dengan memisahkan lapisan presentasi, lapisan domain, dan lapisan data, sehingga menjadi lebih mudah dalam memodifikasi dan memperluas kode tanpa menambahkan kompleksitas yang tidak perlu. Clean Architecture yang diterapkan dalam proyek ini terdiri dari 4 layer, yaitu models, repositories, services, dan controllers.
![clean_architecture](https://github.com/praditauniversity/ReadMe-Ospro/assets/110759186/f73f42a6-f33f-4a22-ac11-4ebce0673e84)
- Models layer: tempat untuk menginisiasi nama kolom beserta tipe data dan relasinya dengan kolom lain dalam database. 
- Repository layer: lapisan yang mengoperasikan kueri untuk penyimpanan dan pengambilan data dengan terhubung langsung ke dalam database. 
- Service layer: tempat untuk memvalidasi request yang dikirimkan client ke dalam sistem aplikasi dan tempat dimana semua business logic berada. 
- Controller layer: lapisan yang menerima request dari client dan memberikan fungsionalitas yang diperlukan berdasarkan autentikasi tertentu.

Tiap repositori proyek yang telah dibuat akan di deploy menggunakan Docker menjadi beberapa container. Tiap Docker container memiliki dua Docker images didalamnya, yaitu fungsi aplikasi dan basis data aplikasi. Lalu untuk komunikasi antar microservices, menggunakan protokol REST API dengan port tertentu yang telah di inisiasi dalam masing-masing repositori proyek (dapat dilihat dalam .env di tiap repo).
> [Go commands](https://dasarpemrogramangolang.novalagung.com/A-go-command.html)<br>
> [CRUD API in Golang](https://www.youtube.com/watch?v=lf_kiH_NPvM)<br>
> [JWT Authentication in Golang](https://www.youtube.com/watch?v=ma7rUS_vW9M)<br>
> [Dependency Injection in Golang](https://www.youtube.com/watch?v=dZ8Ir4Gc8D0&t=137s)<br>
> [Unit Test in Golang](https://www.youtube.com/watch?v=t9QJPE5vwhs&t=1414s)<br>
> [Tutorial membuat web API Golang (FULL)](https://www.youtube.com/watch?v=GjI0GSvmcSU&t=1s)<br>

## Gateway (GraphQL Mesh)
GraphQL yaitu bahasa yang digunakan untuk query API, yang juga menghubungkan sisi depan website atau client kepada sistem database atau backend untuk melakukan operasi atau kueri seperti menampilkan, menambahkan, menyunting, dan menghapus data.
