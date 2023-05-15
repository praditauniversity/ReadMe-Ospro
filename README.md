# READ ME FIRST TO RUN OSPRO APPLICATION
Tutorial untuk menjalankan OSPRO pada lokal server

Semua microservice yang berada pada repository untuk aplikasi OSPRO dapat di jalankan di lokal connection.

Cara menjalankan ospro application

## Tutorial 
Repository pada github untuk aplikasi ospro dibagi menjadi tiga yaitu Backend, Gateway dan Frontend.
- Repository Backend : [ms-user-management](https://github.com/praditauniversity/ms-user-management), [ms-project](https://github.com/praditauniversity/ms-project), [ms-gantt](https://github.com/praditauniversity/ms-gantt), [ms-activity](https://github.com/praditauniversity/ms-activity), [ms-dailyreport](https://github.com/praditauniversity/ms-dailyreport), [ms-report](https://github.com/praditauniversity/ms-report), dsb. (Semua yang bernama ms (microservice))
- Repository Gateway : [gateway](https://github.com/praditauniversity/gateway)
- Repository Frontend : [mf-main](https://github.com/praditauniversity/mf-main)

Lakukanlah penarikan pada repositori-repositori di atas untuk menjalankan aplikasi OSPRO. Dapat dilakukan melalui [GitHub Desktop](https://desktop.github.com/) atau [GitHub di command line](https://cli.github.com/).

Setelah melakukan penarikan pada repository yang sudah disebut lakukan langkah selanjutnya yaitu instalasi [Docker](https://www.docker.com/), [Golang](https://docs.studygolang.com/doc/install), [PostgreSQL](https://www.postgresql.org/download/), [NodeJs](https://nodejs.org/en/download).


## Instalasi Docker
Download [Docker](https://www.docker.com/), pilih lah sesuai dengan sistem operasi yang anda gunakan seperti windows atau linux
jika anda menginstall menggunakan windows anda perlu melakukan beberapa langkah lagi untuk dapat menjalankan docker 
pergi menuju microsoft store kemudian cari alpine setelah itu carilah aplikasi yang bernama Alpine WSL kemudian download 
atau lalu ikuti tutorial di [Install Docker](https://www.petanikode.com/docker-install/)

## How to Build Docker Image dan Run Docker  
Buka visual studio code lalu buka folder ms-project atau ms lainnya 
Buka terminal pada visual studio code 
lalu pada command prompt tuliskan ```docker compose up --build``` (artinya membuild image docker dan melakukan running pada aplikasi docker).
Untuk melakukan docker berjalan pada background application lakukan ```docker compose up --build -d``` (artinya mem-build docker image dan melakukan running pada aplikasi docker dilakukan pada background aplikasi).
Untuk mematikan docker yang sedang berjalan lakukan ```docker compose down```. 
Untuk menghilangkan seluruh data aplikasi beserta database di docker lakukan ```docker compose down -v```. 
Lakukan setiap hal ini pada semua microservice, gateway, frontend yang ingin dijalankan.

## How to Remove Unused Docker
```bash
# Displays information regarding the amount of disk space used by the docker daemon.
docker system df
docker system df -v
```
```bash
# Delete old docker processes
docker rm docker ps -a | grep Exited | awk '{print $1 }' ignore_errors: true
```
```bash
# Delete old images. will complain about still-in-use images
docker rmi docker images -aq
```
```bash
# To remove all images which are not used by existing containers, use the -a flag:
docker image prune -a
```
```bash
# List and remove unused (dangling) volumes in Docker (the content of /var/lib/docker/volumes)
docker volume ls -q -f "dangling=true"
docker volume rm $(docker volume ls -q -f "dangling=true")
```

## Golang Tutorial (Backend)
Dalam setiap repositori proyek, diimplementasikan Clean Architecture yaitu merupakan pola desain perangkat lunak dengan memisahkan lapisan presentasi, lapisan domain, dan lapisan data, sehingga menjadi lebih mudah dalam memodifikasi dan memperluas kode tanpa menambahkan kompleksitas yang tidak perlu. Clean Architecture yang diterapkan dalam proyek ini terdiri dari 4 layer, yaitu models, repositories, services, dan controllers.

![clean_architecture](https://github.com/praditauniversity/ReadMe-Ospro/assets/110759186/f73f42a6-f33f-4a22-ac11-4ebce0673e84)

- Models layer: tempat untuk menginisiasi nama kolom beserta tipe data dan relasinya dengan kolom lain dalam database. 
- Repository layer: lapisan yang mengoperasikan kueri untuk penyimpanan dan pengambilan data dengan terhubung langsung ke dalam database. 
- Service layer: tempat untuk memvalidasi request yang dikirimkan client ke dalam sistem aplikasi dan tempat dimana semua business logic berada. 
- Controller layer: lapisan yang menerima request dari client dan memberikan fungsionalitas yang diperlukan berdasarkan autentikasi tertentu.

Tiap repositori proyek yang telah dibuat akan di deploy menggunakan Docker menjadi beberapa [container](https://www.docker.com/resources/what-container/). Tiap Docker container memiliki dua Docker images didalamnya, yaitu fungsi aplikasi dan basis data aplikasi. Lalu untuk komunikasi antar microservices, menggunakan protokol REST API dengan port tertentu yang telah di inisiasi dalam masing-masing repositori proyek (dapat dilihat dalam .env di tiap repo).
> [CRUD API in Golang](https://www.youtube.com/watch?v=lf_kiH_NPvM)<br>
> [JWT Authentication in Golang](https://www.youtube.com/watch?v=ma7rUS_vW9M)<br>
> [Dependency Injection in Golang](https://www.youtube.com/watch?v=dZ8Ir4Gc8D0&t=137s)<br>
> [Unit Test in Golang](https://www.youtube.com/watch?v=t9QJPE5vwhs&t=1414s)<br>
> [Tutorial membuat web API Golang (FULL)](https://www.youtube.com/watch?v=GjI0GSvmcSU&t=1s)<br>

Jalankan ```go mod tidy``` untuk memvalidasi dependensi (yang ada pada file go.mod). Jika ada dependensi yang belum ter-download, maka akan otomatis di-download. Selengkapnya dapat dilihat di [Go commands](https://dasarpemrogramangolang.novalagung.com/A-go-command.html)

Untuk membuat repositori untuk microservice baru, dapat mengikuti template project di [Project Template](https://github.com/praditauniversity/ms-scaffold)

## Postman
Download [Postman](https://www.postman.com/downloads/) atau Buka melalui [Postman Web](https://web.postman.co/home)

Untuk mengakses Workspace OSPRO
<details> 
  <summary>Sign in with Google Account</summary>
  Gmail: livelycomet@gmail.com <br>
  Password: SmartLiving#123
</details>

Kemudian pilih Workspace yang bernama Living Comet, anda dapat melihat api test untuk tiap microservice pada sidebar collections atau juga pada sidebar APIs di folder ospro.

> [Testing REST APIs using Postman and Newman](https://dev.to/sivalabs/testing-rest-apis-using-postman-and-newman-1hhp)

Untuk tata cara penulisan tests script di Postman, dapat dilihat di [Writing Tests](https://learning.postman.com/docs/writing-scripts/test-scripts/) <br>
Untuk dokumentasi flow API testing OSPRO, dapat dilihat di [Flow Test](https://github.com/praditauniversity/flow-test-reports)

## GraphQL Mesh (Gateway)
GraphQL yaitu bahasa yang digunakan untuk query API, yang juga menghubungkan sisi depan website atau client kepada sistem database atau backend untuk melakukan operasi atau kueri seperti menampilkan, menambahkan, menyunting, dan menghapus data.
> [GraphQL Mesh as a Gateway](https://www.youtube.com/watch?v=fhTg5wPU5LY) <br>
> [Informasi Selengkapnya lihat di repo Gateway](https://github.com/praditauniversity/gateway/blob/main/README.md)

## Instalasi React JS (Frontend)
Sebelum melakukan instalasi React JS, diperlukan instalasi Node JS terlebih dahulu. Untuk download Node JS dapat menggunakan link pada Tutorial diatas atau dengan menggunakan link berikut [NodeJs](https://nodejs.org/en/download). Setelah selesai install Node JS, diperlukan tahap-tahap berikut untuk melakukan instalasi React JS dengan npm:
- Cek Versi dari NPM yaitu dengan menggunakan commmand ```npm -v```

  Jika masih belum ada project react JS, anda dapat membuat project react baru dengan tahapan berikut:
  - Install React dengan mengetik kode: ```npm install -g create-react-app```
  - Untuk mengecek proses instalasinya, bisa dilakukan dengan mengetik: ```create-react-app –version```
  - Jika proses instalasi sudah selesai, kamu bisa membuat project React JS pertamamu. Caranya, ketik:
  ```create-react-app web-react-baru``` (Kamu bisa mengganti “web-react-baru” dengan nama project yang lain) ```cd web-react-baru```
  - Setelah proses pembuatan projectnya selesai, akan ada halaman web dengan alamat localhost:3000 yang terbuka secara otomatis

- Tahap berikutnya jalankan command: ```npm install``` lalu ```npm start```
  <details> 
  <summary>npm install & npm start</summary>
  
    - ```npm install``` (Perintah ini menginstall semua paket/dependencies apa pun yang bergantung pada project) | Jika ```npm install``` tidak berfungsi dengan baik, dapat menambahkan command ```--legacy-peer-deps``` setelah ```npm install``` seperti berikut ini: ```npm install --legacy-peer-deps```
  
    - ```npm start``` (menjalankan aplikasi / React JS)
  </details>


## Instalasi Apollo Client & GraphQL
Apollo Client adalah pustaka manajemen status komprehensif untuk JavaScript yang memungkinkan Anda mengelola data lokal dan jarak jauh dengan GraphQL. Apollo Client digunakan untuk mengambil, meng-cache, dan memodifikasi data aplikasi, sambil memperbarui UI Anda secara otomatis. Berikut dokumentasi [Apollo Client](https://www.apollographql.com/docs/react/)

Install Apollo Client
- Jalankan command ```npm install @apollo/client``` atau ```npm install @apollo/client --legacy-peer-deps```

GraphQL adalah sebuah bahasa query yang digunakan untuk mengambil dan memanipulasi data. Dalam GraphQL, klien dapat mengirimkan permintaan spesifik yang mencakup data yang diperlukan. Ini memungkinkan klien untuk mendapatkan data yang tepat yang mereka inginkan, menghindari masalah over-fetching (mengambil data yang tidak diperlukan) atau under-fetching (mengambil data yang kurang). GraphQL menggunakan skema yang didefinisikan dengan jelas untuk mendefinisikan tipe data yang tersedia dan operasi yang dapat dilakukan pada data tersebut. Berikut dokumentasi [GraphQL](https://graphql.org/code/)

Install GraphQL
- Jalankan command ```npm install graphql``` atau ```npm install graphql --legacy-peer-deps```

## Tutorial & Tips untuk ReactJS
Berikut merupakan tutorial dan juga tips yang dapat berguna untuk mengembangkan project ReactJS anda.

### GraphQL Apollo JWT
- https://flaviocopes.com/graphql-auth-apollo-jwt-cookies/
- https://hasura.io/blog/best-practices-of-using-jwt-with-graphql/

### Fragment
- https://www.apollographql.com/docs/react/data/fragments/

### Cookie
- https://www.npmjs.com/package/js-cookie
- https://www.youtube.com/watch?v=YPgMnugXBJo
- https://medium.com/@ryanchenkie_40935/react-authentication-how-to-store-jwt-in-a-cookie-346519310e81

### React Tutorial
- [useEffect](https://www.youtube.com/watch?v=bGzanfKVFeU)
- [useEffect vs useRef](https://blog.logrocket.com/usestate-vs-useref/)
- [Callback & Promise](https://linuxhint.com/callback-promise-javascript-examples/)

### Write Code Faster
- https://www.youtube.com/watch?v=ph65TPiNmKo 

### Gantt Chart
  #### Create React Gantt Chart
  - https://www.youtube.com/watch?v=AVRHgXQ0g_k
  - https://dhtmlx.com/blog/create-react-gantt-chart-component-dhtmlxgantt/

  #### Specify Column Gantt Chart
  - https://www.youtube.com/watch?v=-BoznxJmJIo

  #### Setting up Scale Gantt
  - https://docs.dhtmlx.com/gantt/desktop__configuring_time_scale.html#timeunits

  #### Custom DHTMLX Add Input
  - https://docs.dhtmlx.com/gantt/desktop__custom_editor.html

  #### add Scurve
  - https://dhtmlx.com/blog/dhtmlxgantt-6-1-time-constraints-backward-scheduling-s-curve/

  #### add custom element
  - https://dhtmlx.com/blog/add-custom-elements-grid-javascript-gantt-dhtmlx-gantt-video-tutorial/
  - https://docs.dhtmlx.com/gantt/desktop__custom_editor.html


### GraphQL - Apollo Client
- https://www.youtube.com/watch?v=YyUWW04HwKY

## Selamat Mencoba salam kami dari angkatan 19 dan 21 yang membuat project ini. Kami harap kalian mendapatkan pengalaman yang banyak setelah melakukan pengembangan aplikasi ini. Good luck and wish you all the best!

Untuk mau bertanya tanya tentang project ini, we are very welcome. Berikut kontak email kami :

projectmanagementospro@gmail.com

### Backend
- Stephen Winata (stephenwinata23@gmail.com)
- Brian Mikhael (brian.mikhael@student.pradita.ac.id)

### Frontend
- Christoper Jordan (christoper.jordan@student.pradita.ac.id)
- Phance Karyadi (phance.karyadi@student.pradita.ac.id)
