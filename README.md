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
> [GraphQL Mesh as a Gateway](https://www.youtube.com/watch?v=fhTg5wPU5LY)

# Query Graphql 
Query dalam menampilkan, menambahkan, menyunting, dan menghapus data pada Graphql
Menampilkan Graphql pada postman
```bash
query project { 
    project {
        Data {
            ID
            name
            description
            user_id
            progress_percentage
            budget_health
            cost_actual
            cost_plan
            budget
            project_objectives
            potential_risk
            start_project
            end_project
            participants
            project_duration
            total_man_power
        }
    }
} 
```

Menambahkan data melalui graphql pada postman
```bash
mutation addProject(
    $status: String!
    $work_area: String!
    $start_project: DateTime!
    $stakeholder_ammount: Int!
    $role_id: Int!
    $type_id: Int!
    $considered_success_when: String!
    $cost_actual: Float!
    $cost_plan: Float!
    $client: String!
    $client_contact: String!
    $currency_name: String!
    $currency_code: String!
    $currency_symbol: String!
    $description: String!
    $end_project: DateTime!
    $name: String!
    $office_location: String!
    $phase_id: Int!
    $potential_risk: [String]!
    $total_man_power: Int!
    $project_objectives: [String]!
    $progress_percentage: Float!
    $budget: Int!
    $participants: Int!
    $available_resources:[String]!
    $milestone_id: Int!
) {
  addProject(
    input: {
    status: $status
    work_area: $work_area
    start_project: $start_project
    stakeholder_ammount: $stakeholder_ammount
        role_id: $role_id
        type_id: $type_id
        considered_success_when: $considered_success_when
        cost_actual: $cost_actual
        cost_plan: $cost_plan
        client: $client
        client_contact: $client_contact
        currency_name: $currency_name
        currency_code: $currency_code
        currency_symbol: $currency_symbol
        description: $description
        end_project: $end_project
        name: $name
        office_location: $office_location
        phase_id: $phase_id
        potential_risk: $potential_risk
        total_man_power: $total_man_power
        project_objectives: $project_objectives
        progress_percentage: $progress_percentage
        budget: $budget
      participants: $participants,
      available_resources: $available_resources,
      milestone_id: $milestone_id
    }
  ) {
    Data {
        ID
        participants
        available_resources
        milestone_id
    }
  }
}
```

Untuk dapat mengganti data liat pada postman kemudian lihat pada graphql variabel
di bawah ini adalah data yang akan di insert
```bash
{
    "status" :"None",
    "work_area":"Tangerang",
    "start_project":"2023-01-05T11:04:48.377+07:00",
    "stakeholder_ammount":100,
    "role_id":10,
    "type_id":2,
    "considered_success_when": "All is Done",
    "cost_actual":8.8,
    "cost_plan":6.7,
    "client": "stephen",
    "name": "Project S",
    "total_man_power": 300,
    "client_contact":"082222",
    "currency_name": "Indonesian Rupiahs",
    "currency_code": "IDR",
    "currency_symbol": "IDR",
    "description": "A Project of anomaly",
    "end_project": "2023-03-13T11:04:48.377+07:00",
    "office_location": "Other Dimesions",
    "phase_id": 2,
    "potential_risk":["good","bad"],
    "project_objectives":["Good","BAD"],
    "progress_percentage": 10.5,
    "budget": 56000,
    "participants": 17,
    "available_resources":["lab","kom"],
    "milestone_id": 2
}
```

Melakukan Update pada graphql pada postman
Diambil dengan ID Project yang mau di update
```bash
mutation updateProject (
    $id: String!
    $name: String!,
    $description: String!,
    $status :String!,
    $work_area :String!,
    $start_project :DateTime,
    $stakeholder_ammount : Int!,
    $role_id : Int!,
    $type_id: Int!,
    $considered_success_when:String!,
    $cost_actual:Float!,
    $cost_plan :Float!,
    $client : String!,
    $client_contact:String!,
    $currency_name:String!,
    $currency_code : String!,
    $currency_symbol :String!,
    $end_project : DateTime,
    $office_location : String!,
    $phase_id: Int!
    $potential_risk : [String]!,
    $project_objectives:[String]!,
    $progress_percentage: Float!,
    $budget:Int!,
    $total_man_power:Int!,
    $available_resources:[String]!,
    $participants: Int!
    ) {
  updateProject( id: $id
  input:{
      name: $name,
      description: $description,
      status: $status, 
      work_area: $work_area, 
      start_project: $start_project,
      stakeholder_ammount: $stakeholder_ammount,
      role_id: $role_id,
      type_id: $type_id,
      considered_success_when: $considered_success_when,
      cost_actual: $cost_actual,
      cost_plan: $cost_plan,
      client:$client,
      client_contact:$client_contact,
      currency_name: $currency_name,
      currency_code: $currency_code,
      currency_symbol: $currency_symbol,
      end_project: $end_project,
      office_location: $office_location,
      phase_id: $phase_id,
      potential_risk: $potential_risk,
      project_objectives: $project_objectives,
      progress_percentage: $progress_percentage,
      budget: $budget,
      total_man_power: $total_man_power,
      participants: $participants,
      available_resources: $available_resources
  }
  ) {
    Data {
        ID
        name
        description
    }
  }
}
```
Data yang perlu untuk menggantikan isi data pada id 1
Dibawah ini adalah variabel graphql
```bash
{
    "id": "1",
    "stakeholder_ammount": 1000,
  "name": "Win Pro",
  "start_project":"2022-10-20T04:04:48.377Z",
  "end_project":"2022-10-20T04:04:48.377Z",
  "work_area":"jakarta",
  "office_location":"gedung 1",
  "cost_plan":10.23,
  "cost_actual":10.11,
  "client":"stephen",
  "client_contact":"081222022",
  "company":"testing",
  "role_id":1,
  "progress_percentage":30.10,
  "description": "Material is needed to create an anomaly.",
  "total_man_power":200,
  "status":"working",
  "project_objectives": ["make everything good", "increase efficiency"],
  "considered_success_when":"all good",
  "potential_risk": ["deadline late", "engagement failure", "run of budget"],
  "currency_symbol":"$",
  "currency_code":"$",
  "currency_name":"dollar",
  "phase_id":1,
  "type_id": 1,
  "budget": 300000,
    "available_resources":["lab","lala"],
    "participants": 17
}
```

Melakukan Delete pada graphql melalui postman
```bash
mutation deleteProject {
  deleteProject(id: "1")
}
```

## Gateway
Pada kodingan gateway untuk dapat menjalankan graphql jika mau menambahkan mutation atau query baru perlu dilakukannya 
Buat lah File yang diletakan pada src/json-schemas
lalu buat file yang ingin anda buat cth seperti activity
kemudian day ini buatlah 2 file json yang diperlukan yaitu request dan response 
request dan response biasa diambil dari query postman pada local tanpa menggunakan graphql
```bash
cth activity-request.json 
{
    "parent_id": 0,
    "gantt_id" : 1,
    "name": "zakhira",
    "description": "Material is needed to create an anomaly.",
    "start_time": "2022-08-09T04:04:48.377Z",
    "end_time": "2022-10-20T04:04:48.377Z",
    "weight_percentage": 50.01,
    "progress_percentage": 50.01,
    "priority": "high",
    "cost_plan": 100000.01,
    "cost_actual": 100000.01,
    "material_cost_plan": 100000.01,
    "material_cost_actual": 100000.01,
    "tool_cost_plan": 100000.01,
    "tool_cost_actual": 100000.01,
    "human_cost_plan": 100000.01,
    "human_cost_actual": 100000.01,
    "activity_type": "manoverpowered",
    "phase_id": 1,
    "unitofmeasurement_id": 1
}
```

Untuk membuat activity response maka response ketika kita sudah berhasil melakukan query tersebut seperti 
```bash
{
    "data": [
        {
            "ID": 1,
            "CreatedAt": "2023-01-25T17:35:00.73698+07:00",
            "UpdatedAt": "2023-01-25T17:35:00.73698+07:00",
            "DeletedAt": null,
            "parent_id": 0,
            "name": "Wepytypur",
            "description": "Material is needed to create an anomaly.",
            "gantt_id": 1,
            "start_time": "2023-01-17T11:04:48.377+07:00",
            "end_time": "2023-02-19T11:04:48.377+07:00",
            "activity_duration": 33,
            "user_id": "dc9076bb-2fda-4019-bd2c-900a8284b9bb",
            "updated_by": "",
            "deleted_by": "",
            "cost_actual": 1.3,
            "cost_plan": 1.3,
            "weight_percentage": 5.3,
            "progress_percentage": 5.3,
            "priority": "High",
            "material_cost_plan": 1.3,
            "material_cost_actual": 1.3,
            "tool_cost_plan": 1.3,
            "tool_cost_actual": 1.3,
            "human_cost_plan": 1.3,
            "human_cost_actual": 1.3,
            "activity_type": "overmantu",
            "phase_id": 1,
            "phase": {
                "ID": 1,
                "CreatedAt": "2023-01-25T17:30:47.322461+07:00",
                "UpdatedAt": "2023-01-25T17:30:47.322461+07:00",
                "DeletedAt": null,
                "name": "Todo",
                "color": "#E54C00",
                "order": 77,
                "user_id": "dc9076bb-2fda-4019-bd2c-900a8284b9bb",
                "updated_by": "",
                "deleted_by": ""
            },
            "unitofmeasurement_id": 1,
            "unitofmeasurement": {
                "ID": 1,
                "CreatedAt": "2023-01-25T17:29:19.999294+07:00",
                "UpdatedAt": "2023-01-25T20:10:52.489524+07:00",
                "DeletedAt": null,
                "name": "Human",
                "description": "Material is needed to create an anomaly.",
                "user_id": "dc9076bb-2fda-4019-bd2c-900a8284b9bb",
                "updated_by": "SUp3R4Dm1n",
                "deleted_by": ""
            }
        }
    ]
}
```

Kemudian tahap selanjutnya masuk ke meshrc.yml
buat lah activity seperti ini 
```bash
- name: activity (nama dari microservice atau querynya)
    handler:
      jsonSchema:
        baseUrl: http://localhost:1007/api/v1/ (nama dari api microservice)
        schemaHeaders:
          Authorization: "{context.headers['authorization']}" (code jwt token untuk auhorization)
        operationHeaders:
          Authorization: "{context.headers['authorization']}"(code jwt token untuk auhorization)
```
```bash
operations:
          - type: Query
            field: activity
            path: /activity/{args.id}
            method: GET
            argTypeMap:
              id:
                type: string
            responseSample: ./src/json-schemas/activity/activity-response.json
        untuk operation di atas yang mengartikan metode get dengan query yang mengambil data activity
```

Untuk operation add,update dan delete lihat di bawah ini 
```bash
type: Mutation
            field: addActivity
            path: /activity
            method: POST
            requestSample: ./src/json-schemas/activity/activity-request.json
            responseSample: ./src/json-schemas/activity/activity-response.json
          - type: Mutation
            field: updateActivity
            path: /activity/{args.id}
            method: PUT
            argTypeMap:
              id:
                type: string
                nullable: false
            requestSample: ./src/json-schemas/activity/activity-request.json
            responseSample: ./src/json-schemas/activity/activity-response.json
          - type: Mutation
            field: deleteActivity
            path: /activity/{args.id}
            method: DELETE
            argTypeMap:
              id:
                type: string
                nullable: false
```
Typenya berubah menjadi mutation lalu gunakan metode seusai dengan fungsinya ingat selalu samakan request dan response jika itu 2 hal salah maka sering terjadi 
error pada bagian tersebut CTH
pada data request ada data sebanyak ini 
```bash
{
    "parent_id": 0,
    "gantt_id" : 1,
    "name": "zakhira",
    "description": "Material is needed to create an anomaly.",
    "start_time": "2022-08-09T04:04:48.377Z",
    "end_time": "2022-10-20T04:04:48.377Z",
    "weight_percentage": 50.01,
    "progress_percentage": 50.01,
    "priority": "high",
    "cost_plan": 100000.01,
    "cost_actual": 100000.01,
    "material_cost_plan": 100000.01,
    "material_cost_actual": 100000.01,
    "tool_cost_plan": 100000.01,
    "tool_cost_actual": 100000.01,
    "human_cost_plan": 100000.01,
    "human_cost_actual": 100000.01,
    "activity_type": "manoverpowered",
    "phase_id": 1,
    "unitofmeasurement_id": 1
}
```
namun pada response ada data seperti ini 
```bash
{
    "data": [
        {
            "ID": 1,
            "CreatedAt": "2023-01-25T17:35:00.73698+07:00",
            "UpdatedAt": "2023-01-25T17:35:00.73698+07:00",
            "DeletedAt": null,
            "parent_id": 0,
            "name": "Wepytypur",
            "description": "Material is needed to create an anomaly.",
            "gantt_id": 1,
            "start_time": "2023-01-17T11:04:48.377+07:00",
            "end_time": "2023-02-19T11:04:48.377+07:00",
            "activity_duration": 33
                 }
    ]
}
```
Maka Data tidak akan di akses karna data yang kurang

pastikan juga dalam sebelum penulisan response {} kurung kurawal paling awal sebelum memulai data dan pastikan isi data menggunakan lambang [].

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

## Selamat Mencoba salam kami dari angakatan 19 dan 21 yang membuat project ini Kami harap kalian mendapatkan pengalaman yang banyak setelah melakukan pengerjaan aplikasi ini Good luck and wish you all the best 
Untuk mau bertanya tanya tentang project ini we are very welcome kontak email kami :

### Backend
- Stephen Winata (stephenwinata23@gmail.com)

### Frontend
- Christoper Jordan (christoper.jordan@student.pradita.ac.id)
- Phance Karyadi (phance.karyadi@student.pradita.ac.id)
