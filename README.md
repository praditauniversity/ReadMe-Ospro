# READ ME FIRST TO RUN OSPRO APPLICATION
Tutorial untuk menjalankan Ospro pada lokal server

Semua microservice yang berada pada repository untuk aplikasi ospro dapat di jalankan di lokal connection.
Cara menjalankan ospro application
## Tutorial 
Repository pada github untuk aplikasi ospro dibagi menjadi tiga yaitu Backend, Gateway dan Frontend
Repository Backend : ms-project,ms-gantt,ms-activity,ms-dailyreport,ms-report,ms-user-management. Semua yang beranama ms (microservice) itu adalah bagian dari backend
Repository Gateway : gateway
Repository Frontend : mf-main

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
lalu pada command prompt tuliskan ```docker compose up --build``` (artinya membuild image docker dan melakukan running pada aplikasi docker)
untuk melakukan docker berjalan pada background application lakukan ```docker compose up --build -d``` (artinya membuild image docker dan melakukan running pada aplikasi docker dilakukan pada background aplikasi)
Untuk mematikan docker yang sedang berjalan lakukan ```docker compose down```. 
Untuk menghilangkan seluruh data aplikasi beserta database di docker lakukan ```docker compose down -v```. 
Lakukan setiap hal ini pada semua microservice, gateway, forntend yang ingin di jalankan

