# READ ME FIRST
## Unfinished Project Progress
### Notes (Bagian ini beriskan progress-progress yang belum di implementasikan dalam project ini)
- Belum ada Role pada user management (Hal ini dibutuhkan untuk membedakan level/tingkat otoritas yang dapat dilakukan oleh user terhadap project)
- Export file dari project yang berbentuk dokumen, seperti Minutes of Meeting, Daily Report, Project Charter, dan lain sebagainya yang berbentuk dokumen.
- Fitur Import / Upload file
- Advance UI (ini berisikan customize tampilan komponen yang dapat diubah-ubah oleh user seperti penambahan, perubahan ukuran, pemindahan)
- Berhubungan dengan account (Reset Password, Forget Password, username, email, dan lain sebagainya)
- Edit Profile (Belum dapat melakukan perubahan data-data pada user karena belum ada database yang menyimpan data-data user)
- Login dengan authentikasi lain (Seperti Google, Facebook, dan lain sebagainya)
- Verifikasi email (dikirimkan email verifikasi seperti code)
- Komponen sudah dibuat namun belum terkoneksi dengan database:
  1. Chart Project Progress
  2. Issue
  3. SCurve
  4. Manpower
  5. Daily Reminder
  6. Kalender
  7. Jam
- Gantt Chart yang berhubungan dengan:
  1. Fitur antar activity, dimana subactivity mengikuti range timeline dari mainactivity sehingga tidak bisa dibuat untuk tanggal sebelum atau sesudah main activity termasuk ketika melakukan update dan delete. Misalnya update mainactivity akan otomatis mengganti subactivity juga.
  2. Fitur Link (garis kuning penghubung activity) batasan dimana jika tanggal awal Activity A setelah tanggal akhir Activity B maka activity A tidak bisa diberikan Link yang mengharuskan Activity A dikerjakan terlebih dahulu sebelum ke Activity B karena berdasar timeline Activity B lebih dahulu.
  3. Fitur assignment activity untuk menambahkan user/anggota tim yang ditugaskan untuk activity tersebut pada sebuah project
  4. Fitur seperti kotak ceklis atau tombol untuk mengubah status activity

## HOW TO RUN OSPRO APPLICATION
Arsitektur aplikasi web OSPRO yang digunakan ialah arsitektur microservices yang merupakan model arsitektur yang memisahkan aplikasi menjadi beberapa komponen yang independen dan diimplementasikan sebagai aplikasi yang dapat berdiri sendiri, dikembangkan, di deploy, dan diubah secara independen tanpa mempengaruhi komponen lainnya. Dengan menerapkan arsitektur microservices, jika salah satu bagian dari aplikasi mengalami masalah, hanya bagian tersebut yang terpengaruh, sehingga mengurangi dampaknya pada keseluruhan sistem. <br><br>
Tiap microservices ditampung ke dalam suatu docker container. Tiap Docker container memiliki dua Docker images didalamnya, yaitu fungsi aplikasi dan basis data aplikasi dari suatu microservices. Jadi tiap microservices memiliki database tersendiri yang ditampung dalam container. <br><br>
Dalam pengelolaan data dari masing-masing microservices digunakan GraphQL sebagai penghubung dari database pada tiap microservice berdasarkan API masing-masing ke sisi depan (Frontend).

## Tutorial 
Repository pada github untuk aplikasi ospro dibagi menjadi tiga yaitu Backend, Gateway dan Frontend.
- Repository Backend : [ms-user-management](https://github.com/praditauniversity/ms-user-management), [ms-project](https://github.com/praditauniversity/ms-project), [ms-gantt](https://github.com/praditauniversity/ms-gantt), [ms-activity](https://github.com/praditauniversity/ms-activity), [ms-dailyreport](https://github.com/praditauniversity/ms-dailyreport), [ms-report](https://github.com/praditauniversity/ms-report), dsb. (Semua yang bernama ms (microservice))
- Repository Gateway : [gateway](https://github.com/praditauniversity/gateway)
- Repository Frontend : [mf-main](https://github.com/praditauniversity/mf-main)

Lakukanlah penarikan pada repositori-repositori di atas untuk menjalankan aplikasi OSPRO. Dapat dilakukan melalui [GitHub Desktop](https://desktop.github.com/) atau [GitHub di command line](https://cli.github.com/).

Setelah melakukan penarikan pada repository yang sudah disebut lakukan langkah selanjutnya yaitu melakukan penginstallan berikut:
- [Docker](https://www.docker.com/) <br> Pilihlah sesuai dengan sistem operasi yang anda gunakan, seperti windows atau linux. Jika anda menginstall menggunakan windows, anda akan disuruh menginstall WSL 2 atau anda dapat melakukan instalasi [Alpine WSL](https://apps.microsoft.com/store/detail/alpine-wsl/9P804CRF0395?hl=en-id&gl=id&rtc=1), atau selengkapnya lihat di [How to install Docker on Windows](https://medium.com/devops-with-valentine/how-to-install-docker-on-windows-10-11-step-by-step-83074a80e6f9)
- [Golang](https://docs.studygolang.com/doc/install)
- [PostgreSQL](https://www.postgresql.org/download/)
- [NodeJs](https://nodejs.org/en/download).
- [Yarn](https://classic.yarnpkg.com/lang/en/docs/install/#windows-stable)

Install docker image berikut:
- [postgres](https://hub.docker.com/_/postgres), atau [How To Install and Run PostgreSQL using Docker](https://dev.to/shree_j/how-to-install-and-run-psql-using-docker-41j2)

Selanjutnya pada tiap repository backend, jalankan:
- ```go mod tidy``` untuk memvalidasi dependensi (yang ada pada file go.mod).
- ```docker compose up --build``` atau ```docker compose up --build -d``` (artinya membuild image docker dan melakukan running docker container).
- Untuk repositori [ms-user-management](https://github.com/praditauniversity/ms-user-management), buka terminal baru, lalu lakukan:
  - ```git checkout Staging``` untuk beralih ke branch Staging.
  - ```git pull``` untuk memastikan penarikan kode dalam branch tersebut sudah up to date.
  - Ikuti [Script cli docker psql](https://github.com/praditauniversity/ms-user-management/blob/Staging/cli_script_psql.txt) untuk melakukan insert data Admin.

Pada repository gateway, jalankan:
- ```npm install``` (Perintah ini menginstall semua paket/dependencies apa pun yang bergantung pada project) | Jika ```npm install``` tidak berfungsi dengan baik, dapat menambahkan command ```--legacy-peer-deps``` setelah ```npm install``` seperti berikut ini: ```npm install --legacy-peer-deps```. Jika tetap bermasalah, gunakan command ```yarn install```
- ```npm run dev```

Pada repository frontend, lakukan:
- Sesuaikan untuk IP gateway pada line 18 di [App.jsx](https://github.com/praditauniversity/mf-main/blob/main/src/App.jsx). Misalkan anda menjalankan gateway di localhost, ubah uri menjadi seperti ```uri: "http://localhost:4000/graphql"```
- ```docker compose up``` atau ```docker compose up --build -d```

<br>Jika semua telah berhasil dijalankan, langkah selanjutnya:
### Postman
Download [Postman](https://www.postman.com/downloads/) atau Buka melalui [Postman Web](https://web.postman.co/home)

Untuk mengakses Workspace OSPRO, lakukan:
<details> 
  <summary>Sign in dengan Google Account ini di browser anda</summary>
  Gmail: livelycomet@gmail.com <br>
  Password: SmartLiving#123
</details>

Setelah itu Sign In With Google Account di Postman dengan akun google diatas

Kemudian pilih Workspace yang bernama Living Comet, anda dapat melihat api test untuk tiap microservice pada sidebar collections atau juga pada sidebar APIs di folder ospro.

Setelah itu pertama-tama, navigasi ke sidebar APIs. Pada environment yang berada di bagian kanan atas, pilih ```ms-local-env```. Kemudian pergi ke folder ospro/ProjectManagement, lakukanlah:
- Pada folder user/auth. Pilih ```Auth Login as Admin```, lalu lakukan send request untuk login.
- Pada folder Project/type. Jalankan send request untuk ```Create Project Type```.
- Pada folder Project/phase. Jalankan send request untuk ```Create Project Phase```.
- Pada folder Project/milestone. Jalankan send request untuk ```Create Project Milestone```.
- Pada folder Activity/phase. Jalankan send request untuk ```Create Activity Phase 1-3```.
- Pada folder Activity/UnitOfMeasurement. Jalankan send request untuk ```Create UnitOfMeasurement```.

Anda juga dapat mempelajari:
> [Testing REST APIs using Postman and Newman](https://dev.to/sivalabs/testing-rest-apis-using-postman-and-newman-1hhp) <br>
> [Writing Tests in Postman](https://learning.postman.com/docs/writing-scripts/test-scripts/) <br>

Untuk dokumentasi User Acceptance Test OSPRO, ada di [UAT - OSPRO](https://docs.google.com/spreadsheets/d/1nnqOw3AWtlsLxJXtLjpi1z-q5IWPHYeh3qON04dC8Ik/edit?usp=sharing) <br>
Untuk dokumentasi flow API testing OSPRO, ada di [Flow Test](https://github.com/praditauniversity/flow-test-reports)


## How to Build Docker Image dan Run Docker 
Anda dapat melihat konfigurasi microservices di [Template Microservices](https://github.com/praditauniversity/ms-scaffold).
Dalam file template microservices ini, dalam build docker diperlukan untuk mengkonfigurasi 3 file yang terpenting dalam membuild docker image:
- [.env](https://github.com/praditauniversity/ms-scaffold/blob/main/.env). Berkas .env (environment) adalah berkas konfigurasi yang digunakan untuk menyimpan variabel lingkungan (environment variables) dalam aplikasi. Variabel lingkungan adalah nilai yang dapat digunakan dalam aplikasi untuk mengonfigurasi berbagai aspek, seperti pengaturan aplikasi, pengaturan database, kunci rahasia, koneksi ke layanan eksternal, dan sebagainya. 
Ubah value dari APP_NAME, SERVICE_ID, dan SERVICE_NAME sesuai nama dan kebutuhan microservices.
  ```bash
  # Menentukan nama aplikasi sebagai "MS_SCAFFOLD"
  APP_NAME=MS_SCAFFOLD

  # Menentukan ID service sebagai "1"
  SERVICE_ID=1
  
  # Menentukan nama service sebagai "scaffold"
  SERVICE_NAME=scaffold
  
  # Menentukan zona waktu sebagai "Asia/Jakarta"
  TZ=Asia/Jakarta
  
  # Menentukan mode SSL sebagai "disable"
  SSL_MODE=disable
  
  # Menentukan lingkungan (environment) Go sebagai "test"
  GO_ENV=test
  
  # Menentukan port Go sebagai "8080"
  GO_PORT=8080
  
  # Menentukan direktori data PostgreSQL sebagai "/var/lib/postgresql/data/pgdata"
  PGDATA=/var/lib/postgresql/data/pgdata
  
  # Menentukan pengguna PostgreSQL sebagai "root"
  POSTGRES_USER=root
  
  # Menentukan kata sandi PostgreSQL sebagai "root"
  POSTGRES_PASSWORD=root
  
  # Menentukan nama basis data PostgreSQL berdasarkan nilai dari variabel SERVICE_NAME (dalam contoh ini, "scaffold")
  POSTGRES_DB=${SERVICE_NAME}
  
  # Menentukan kunci rahasia JSON Web Token (JWT) untuk otentikasi sebagai "ac43724f16e9241d990427ab7c8f4228"
  JWT_SECRET_AUTH=ac43724f16e9241d990427ab7c8f4228
  
  # Menentukan kunci rahasia JSON Web Token (JWT) untuk penyegaran sebagai "03b62516184fb6ef591f45bd4974b753"
  JWT_SECRET_REFRESH=03b62516184fb6ef591f45bd4974b753
  
  # Menentukan nama basis data berdasarkan nilai dari variabel POSTGRES_DB (dalam contoh ini, "scaffold")
  DB_NAME=${POSTGRES_DB}
  
  # Menentukan pengguna basis data berdasarkan nilai dari variabel POSTGRES_USER (dalam contoh ini, "root")
  DB_USER=${POSTGRES_USER}
  
  # Menentukan kata sandi basis data berdasarkan nilai dari variabel POSTGRES_PASSWORD (dalam contoh ini, "root")
  DB_PASS=${POSTGRES_PASSWORD}
  
  # Menentukan host basis data sebagai "db"
  DB_HOST=db
  
  # Menentukan port basis data sebagai "5432"
  DB_PORT=5432
  
  # Menentukan port "scaffold" berdasarkan nilai dari variabel SERVICE_ID (dalam contoh ini, "1001")
  SCAFFOLD_PORT=100${SERVICE_ID}
  
  # Menentukan port basis data "scaffold" berdasarkan nilai dari variabel SERVICE_ID (dalam contoh ini, "2001")
  SCAFFOLD_DB_PORT=200${SERVICE_ID}
  ```
- [Dockerfile](https://github.com/praditauniversity/ms-scaffold/blob/main/config/docker/Dockerfile). Dockerfile adalah file teks yang digunakan untuk membangun image Docker. Dockerfile berisi serangkaian perintah yang memberikan instruksi kepada Docker Engine tentang cara membangun image yang akan digunakan untuk menjalankan aplikasi dalam wadah (container) Docker. Ubah 'scaffold' dengan nama microservices baru yang ingin ditambahkan.
  ```bash
  # Menggunakan image golang:alpine sebagai dasar
  FROM golang:alpine
  
  # Membuat direktori /scaffold di dalam container
  RUN mkdir /scaffold
  
  # Mengatur direktori kerja saat ini menjadi /report di dalam container
  WORKDIR /scaffold
  
  # Menambahkan file go.mod ke dalam container di direktori /report
  ADD ./go.mod .
  
  # Menambahkan file go.sum ke dalam container di direktori /report
  ADD ./go.sum .
  
  # Mendownload dependensi yang didefinisikan dalam go.mod
  RUN go mod download
  
  # Menginstall CompileDaemon dari GitHub menggunakan go mod
  RUN go install -mod=mod github.com/githubnemo/CompileDaemon
  
  # Membuat direktori ./bin di dalam container
  RUN mkdir -p ./bin
  
  # Menambahkan semua file yang ada dalam direktori proyek ke dalam container di direktori /scaffold
  ADD . .
  
  # Mengekspos port 8080 dari container
  EXPOSE 8080
  
  # Menjalankan CompileDaemon saat container dimulai
  # -log-prefix=false : Menonaktifkan prefix log
  # -directory="." : Mengawasi direktori saat ini
  # -build="go build -o ./bin/report" : Memanggil go build untuk membangun proyek dan menghasilkan file biner bernama report di dalam direktori /bin
  # -command="./bin/report" : Menjalankan file biner report sebagai perintah utama dalam container
  ENTRYPOINT CompileDaemon -log-prefix=false -directory="." -build="go build -o ./bin/report" -command="./bin/report"
  ```
- [docker-compose.yml](https://github.com/praditauniversity/ms-scaffold/blob/main/docker-compose.yml). Berkas docker-compose.yml digunakan untuk mendefinisikan dan mengelola kumpulan layanan (services) dalam lingkungan Docker menggunakan Docker Compose yang memungkinkan pengguna untuk mendefinisikan dan menjalankan aplikasi yang terdiri dari beberapa kontainer Docker secara terkoordinasi.
Terdapat dua services, yang pertama untuk nama container microservice dan yang kedua untuk nama container database microservice nya. Ubahlah sesuai dengan kebutuhan microservices baru yang ingin anda tambahkan.
  ```bash
  version: "3"  # Versi dari Docker Compose yang digunakan

  services:  # Mendefinisikan layanan dalam aplikasi
    scaffold:  # Layanan bernama "scaffold"
      container_name: ${SERVICE_NAME}  # Nama kontainer yang akan digunakan
      restart: always  # Mengatur kebijakan restart kontainer menjadi "always"
      tty: true  # Mengatur mode terminal untuk kontainer menjadi "true"
      build:  # Konfigurasi untuk membangun kontainer
        context: .  # Konteks build adalah direktori saat ini
        dockerfile: ./config/docker/Dockerfile  # Lokasi Dockerfile yang akan digunakan
      working_dir: /${SERVICE_NAME}  # Direktori kerja dalam kontainer
      volumes:  # Mengaitkan volume antara host dan kontainer
        - .:/${SERVICE_NAME}  # Mengaitkan direktori host saat ini dengan direktori dalam kontainer
      ports:  # Menentukan port yang akan diekspos
        - ${SCAFFOLD_PORT}:8080  # Mengaitkan port host dengan port dalam kontainer
      env_file: .env  # Menggunakan berkas .env untuk mengatur variabel lingkungan
      links:  # Membuat tautan antara kontainer
        - "scaffold_db:db"  # Membuat tautan dengan layanan "scaffold_db"
      depends_on:  # Menentukan dependensi antara layanan
        - scaffold_db  # Menunjukkan bahwa layanan ini bergantung pada layanan "scaffold_db"
  
    scaffold_db:  # Layanan database bernama "scaffold_db"
      container_name: scaffold_db  # Nama kontainer yang akan digunakan
      healthcheck:  # Konfigurasi pemeriksaan kesehatan
        test: ["CMD-SHELL", "pg_isready -U root -d ${SERVICE_NAME}"]  # Perintah untuk memeriksa ketersediaan basis data
        interval: 15s  # Interval antara pemeriksaan kesehatan
        timeout: 1m  # Waktu maksimum untuk menunggu respons pemeriksaan kesehatan
        retries: 5  # Jumlah percobaan pemeriksaan kesehatan yang akan dilakukan
        start_period: 30s  # Waktu yang harus dilewati sebelum memulai pemeriksaan kesehatan
      image: postgres  # Menggunakan image Docker "postgres" sebagai basis untuk kontainer
      restart: always  # Mengatur kebijakan restart kontainer menjadi "always"
      env_file: .env  # Menggunakan berkas .env untuk mengatur variabel lingkungan
      volumes:  # Mengaitkan volume antara host dan kontainer
        - scaffold_db_data:/var/lib/postgresql/data  # Mengaitkan volume yang akan digunakan untuk menyimpan data basis data
      ports:  # Menentukan port yang akan diekspos
        - ${SCAFFOLD_DB_PORT}:5432  # Mengaitkan port host dengan port dalam kontainer
  
  volumes:  # Mendefinisikan volume yang digunakan dalam aplikasi
    scaffold_db_data:  # Volume bernama "scaffold_db_data"
  ```
Selanjutnya buka folder ms-project atau ms-lainnya melalui cmd atau terminal di [Visual Studio Code](https://code.visualstudio.com/download). 
Tuliskan ```docker compose up --build``` (artinya membuild image docker dan melakukan running docker container).
Untuk menjalankan docker container pada background application, lakukan ```docker compose up --build -d``` (artinya mem-build docker image dan melakukan running docker container pada background aplikasi).
Untuk mematikan docker container yang sedang berjalan lakukan ```docker compose down```. 
Untuk menghilangkan seluruh data aplikasi beserta database di docker container lakukan ```docker compose down -v```. 

## How to Open Postgres in Docker Container by Terminal
```bash
# Open a shell session inside a running Docker container named servicename_db (replace servicename_db with the actual service's database name)
docker compose exec servicename_db /bin/sh

# Start the PostgreSQL interactive terminal and connect to the servicename database using the root username (replace servicename with the actual service name)
psql -d servicename -U root

# List all tables in the currently connected database
\dt

# Get information about a specific table named tablename (replace tablename with the actual table name)
\d tablename

# Select all records from a table named dbname(s) (replace dbname(s) with the actual database name)
select * from dbname(s);

# Exit the PostgreSQL interactive terminal
\q

# Exit the shell session within the Docker container and return to the host system's shell prompt
exit

```

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

Tiap repositori proyek yang telah dibuat akan di deploy menggunakan Docker menjadi beberapa [container](https://www.docker.com/resources/what-container/). Tiap Docker container memiliki dua Docker images didalamnya, yaitu fungsi aplikasi dan basis data aplikasi. Lalu untuk komunikasi antar microservices, menggunakan protokol REST API dengan port tertentu yang telah di inisiasi dalam masing-masing repositori proyek (dapat dilihat dalam .env di tiap repo).<br>
Selengkapnya pelajari:
> [CRUD API in Golang](https://www.youtube.com/watch?v=lf_kiH_NPvM)<br>
> [JWT Authentication in Golang](https://www.youtube.com/watch?v=ma7rUS_vW9M)<br>
> [Dependency Injection in Golang](https://www.youtube.com/watch?v=dZ8Ir4Gc8D0&t=137s)<br>
> [Unit Test in Golang](https://www.youtube.com/watch?v=t9QJPE5vwhs&t=1414s)<br>
> [Tutorial membuat web API Golang (FULL)](https://www.youtube.com/watch?v=GjI0GSvmcSU&t=1s)<br>

Jalankan ```go mod tidy``` untuk memvalidasi dependensi (yang ada pada file go.mod). Jika ada dependensi yang belum ter-download, maka akan otomatis di-download. Selengkapnya dapat dilihat di [Go commands](https://dasarpemrogramangolang.novalagung.com/A-go-command.html)

Untuk membuat repositori untuk microservice baru, dapat mengikuti template project di [Project Template](https://github.com/praditauniversity/ms-scaffold)


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


## Selamat Mencoba! Salam kami dari angkatan 19 dan 21 yang membuat project ini. Kami harap kalian mendapatkan pengalaman yang banyak setelah melakukan pengembangan aplikasi ini. Good luck and wish you all the best!

Untuk mau bertanya-tanya tentang project ini, we are very welcome. Berikut kontak email kami :

projectmanagementospro@gmail.com

### Backend
- Hendra Lijaya
- Austin Nicholas
- Stephen Winata (stephenwinata23@gmail.com)
- Brian Mikhael (brian.mikhael@student.pradita.ac.id)

### Frontend
- Patricia Ho
- Christoper Jordan (christoper.jordan@student.pradita.ac.id)
- Phance Karyadi (phance.karyadi@student.pradita.ac.id)
