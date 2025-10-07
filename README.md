# Go CRUD API

โปรเจกต์นี้คือ RESTful API แบบง่ายๆ ที่สร้างด้วยภาษา Go และใช้ `gorilla/mux` สำหรับการจัดการ routing โดย API นี้รองรับการทำงาน CRUD (Create, Read, Update, Delete) สำหรับ "items"

ข้อมูลจะถูกจัดเก็บไว้ในหน่วยความจำ (in-memory) และจะถูกรีเซ็ตทุกครั้งที่รีสตาร์ทแอปพลิเคชัน

## คุณสมบัติ

- **GET /items**: ดึงรายการ items ทั้งหมด
- **GET /items/{id}**: ดึง item ตาม ID
- **POST /items**: สร้าง item ใหม่
- **PUT /items/{id}**: อัปเดต item ที่มีอยู่ตาม ID
- **DELETE /items/{id}**: ลบ item ตาม ID

## ข้อกำหนดเบื้องต้น

- Go (เวอร์ชัน 1.16 หรือสูงกว่า)

## การติดตั้ง

1.  Clone a repository:

    ```bash
    git clone <your-repository-url>
    cd go-crud-app
    ```

2.  ติดตั้ง dependencies:

    ```bash
    go mod tidy
    ```

## การใช้งาน

1.  รันเซิร์ฟเวอร์:

    ```bash
    go run main.go
    ```

2.  เซิร์ฟเวอร์จะเริ่มทำงานที่ `http://localhost:8080`

## API Endpoints

### 1. Get All Items

- **Method**: `GET`
- **URL**: `/items`
- **ตัวอย่างการเรียกใช้งาน (cURL)**:
  ```bash
  curl http://localhost:8080/items
  ```

### 2. Get Item by ID

- **Method**: `GET`
- **URL**: `/items/{id}`
- **ตัวอย่างการเรียกใช้งาน (cURL)**:
  ```bash
  curl http://localhost:8080/items/1
  ```

### 3. Create a New Item

- **Method**: `POST`
- **URL**: `/items`
- **Body (JSON)**:
  ```json
  {
    "name": "New Item Name"
  }
  ```
- **ตัวอย่างการเรียกใช้งาน (cURL)**:
  ```bash
  curl -X POST -H "Content-Type: application/json" -d '{"name":"My New Item"}' http://localhost:8080/items
  ```

### 4. Update an Item

- **Method**: `PUT`
- **URL**: `/items/{id}`
- **Body (JSON)**:
  ```json
  {
    "name": "Updated Item Name"
  }
  ```
- **ตัวอย่างการเรียกใช้งาน (cURL)**:
  ```bash
  curl -X PUT -H "Content-Type: application/json" -d '{"name":"Updated Name"}' http://localhost:8080/items/1
  ```

### 5. Delete an Item

- **Method**: `DELETE`
- **URL**: `/items/{id}`
- **ตัวอย่างการเรียกใช้งาน (cURL)**:
  ```bash
  curl -X DELETE http://localhost:8080/items/1
  ```
