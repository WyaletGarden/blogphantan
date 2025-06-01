---
title: "Blog Deliverable 2"
date: "2025-05-30"
updated: "2025-05-30"
categories:
  - "Deliverable"
coverImage: "/images/sir.jpg"
coverWidth: 16
coverHeight: 9
excerpt: Deliverable 2
---

# Ứng Dụng Danh Bạ Điện Thoại Phân Tán: Xây Dựng Hệ Thống High Availability với Golang

## 1. Giới Thiệu Đề Tài

**Ứng dụng Danh Bạ Điện Thoại Phân Tán** là một hệ thống cho phép lưu trữ và quản lý danh bạ điện thoại trên nhiều máy chủ (nodes) khác nhau, đảm bảo tính sẵn sàng cao (**high availability**), khả năng mở rộng (**scalability**) và tính chịu lỗi (**fault tolerance**).

Hệ thống sử dụng kỹ thuật **sharding** để phân tán dữ liệu và **replication** để sao chép dữ liệu giữa các node, giúp cân bằng tải và đảm bảo dữ liệu không bị mất ngay cả khi một số node gặp sự cố.

---

## 2. Mục Tiêu Của Đề Tài

### 🎯 Các Mục Tiêu Chính

- **Phân tán dữ liệu**: Dữ liệu danh bạ được phân bố đều trên nhiều node để tránh tình trạng quá tải trên một máy chủ duy nhất.

- **Đảm bảo tính nhất quán**: Khi dữ liệu được thêm/sửa/xóa trên một node, nó sẽ tự động đồng bộ với các node khác.

- **Chịu lỗi (Fault Tolerance)**: Nếu một node bị sập, hệ thống vẫn hoạt động bình thường nhờ cơ chế lưu trữ tạm thời (pending data) và tự động đồng bộ khi node phục hồi.

- **Hiệu suất cao**: Nhờ phân tán dữ liệu, hệ thống có thể xử lý nhiều yêu cầu cùng lúc mà không bị nghẽn cổ chai.

---

## 3. Kiến Trúc Hệ Thống

Hệ thống gồm nhiều node (máy chủ), mỗi node có thể đóng vai trò:

### 🏛️ Các Loại Node

- **Primary Node**: Node chính lưu trữ dữ liệu của một số contact dựa trên hàm băm (hash).
- **Backup Node**: Sao lưu dữ liệu từ primary node để đảm bảo dự phòng.

### 📊 Sơ Đồ Kiến Trúc

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Node 1    │    │   Node 2    │    │   Node 3    │
│ (Primary)   │◄──►│ (Backup)    │◄──►│ (Backup)    │
│ Port: 8080  │    │ Port: 8081  │    │ Port: 8082  │
└─────────────┘    └─────────────┘    └─────────────┘
       │                   │                   │
       └───────────────────┼───────────────────┘
                           │
                    ┌─────────────┐
                    │  Load       │
                    │  Balancer   │
                    └─────────────┘
```

---

## 4. Mô Tả Chi Tiết Các Thành Phần

### 4.1. Sharding (Phân Mảnh Dữ Liệu)

**Thuật toán**: Sử dụng **FNV Hash** để xác định primary node.

**Logic hoạt động**:
- Mỗi contact được lưu trên một primary node dựa trên hash của tên.
- **Ví dụ**: Contact "Alice" → Hash → Node 1.

```go
func getNodeForContact(name string) int {
    hash := fnv.New32a()
    hash.Write([]byte(name))
    return int(hash.Sum32()) % totalNodes
}
```

### 4.2. Replication (Sao Chép Dữ Liệu)

- Khi **thêm/sửa** contact, primary node sẽ gửi dữ liệu đến 2 backup nodes thông qua API `/replicate`.
- Khi **xóa** contact, lệnh xóa được gửi đến tất cả các node.

### 4.3. Fault Tolerance (Chịu Lỗi)

- **Pending Data**: Nếu primary node không khả dụng, dữ liệu tạm thời được lưu vào `pending_<name>` và đồng bộ sau.
- **Health Check**: Mỗi node có endpoint `/ping` để kiểm tra trạng thái.

---

## 5. Tính Năng Chính

| Tính Năng | Mô Tả |
|-----------|-------|
| **Thêm Contact** | Dữ liệu được lưu trên primary node và replicate sang backup nodes. |
| **Sửa Contact** | Xử lý cả trường hợp thay đổi tên (có thể thay đổi primary node). |
| **Xóa Contact** | Xóa trên tất cả các node để đảm bảo nhất quán. |
| **Hiển Thị Danh Bạ** | Chỉ hiển thị dữ liệu đã đồng bộ, không hiển thị dữ liệu pending. |
| **Tự Động Phục Hồi** | Khi node sập và khởi động lại, dữ liệu pending được đồng bộ lại. |

---

## 6. Công Nghệ & Thư Viện Sử Dụng

| Công nghệ | Lý do chọn |
|-----------|------------|
| **Golang** | Hiệu suất cao, hỗ trợ concurrent tốt. |
| **Gin Framework** | Nhẹ, phù hợp cho API phân tán. |
| **LevelDB** | Key-Value Store, không cần server riêng. |
| **FNV Hash** | Đơn giản, phân phối dữ liệu đều. |

### 🛠️ Cài Đặt Dependencies

```bash
go mod init distributed-phonebook
go get github.com/gin-gonic/gin
go get github.com/syndtr/goleveldb/leveldb
```

---

## 7. Mô Hình Dữ Liệu (Database Model)

### 📝 Cấu Trúc Dữ Liệu

- **Key**: Tên contact (ví dụ: `Alice`)
- **Value**: Số điện thoại (ví dụ: `0912345678`)
- **Pending Data**: `pending_Alice` → `0912345678`

### 🗂️ Ví Dụ Dữ Liệu

```json
{
  "Alice": "0912345678",
  "Bob": "0987654321",
  "pending_Charlie": "0901234567"
}
```

---

## 8. API Endpoints

### 📡 Danh Sách API

| Method | Endpoint | Mô Tả |
|--------|----------|-------|
| `GET` | `/contacts` | Lấy danh sách tất cả contacts |
| `POST` | `/contacts` | Thêm contact mới |
| `PUT` | `/contacts/:name` | Cập nhật contact |
| `DELETE` | `/contacts/:name` | Xóa contact |
| `GET` | `/ping` | Kiểm tra trạng thái node |
| `POST` | `/replicate` | Đồng bộ dữ liệu giữa nodes |

### 📋 Ví Dụ Request/Response

```bash
# Thêm contact mới
curl -X POST http://localhost:8080/contacts \
  -H "Content-Type: application/json" \
  -d '{"name":"Alice","phone":"0912345678"}'

# Response
{
  "status": "success",
  "message": "Contact added successfully"
}
```

---

## 9. Chiến Lược Triển Khai

### 🧪 Local Testing

Chạy nhiều node trên cùng máy với các port khác nhau:

```bash
# Terminal 1
go run main.go --port=8080 --node-id=1

# Terminal 2  
go run main.go --port=8081 --node-id=2

# Terminal 3
go run main.go --port=8082 --node-id=3
```

### 🚀 Production Deployment

#### Docker Containerization

```dockerfile
FROM golang:1.19-alpine AS builder
WORKDIR /app
COPY . .
RUN go build -o distributed-phonebook .

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /app/distributed-phonebook .
CMD ["./distributed-phonebook"]
```

#### Kubernetes Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: phonebook-node
spec:
  replicas: 3
  selector:
    matchLabels:
      app: phonebook
  template:
    metadata:
      labels:
        app: phonebook
    spec:
      containers:
      - name: phonebook
        image: distributed-phonebook:latest
        ports:
        - containerPort: 8080
```

---

## 10. Kết Luận

### ✅ Ưu Điểm Đạt Được

- **High Availability**: Hệ thống hoạt động liên tục ngay cả khi có node bị lỗi
- **Scalability**: Dễ dàng thêm node mới để mở rộng hệ thống
- **Data Consistency**: Đảm bảo dữ liệu nhất quán trên tất cả các node
- **Performance**: Xử lý đồng thời nhiều request với hiệu suất cao

### 🔮 Hướng Phát Triển

- Implement **Consistent Hashing** để giảm data migration khi thêm/bớt node
- Thêm **Authentication & Authorization** 
- Tích hợp **Monitoring & Logging** với Prometheus/Grafana
- Implement **Auto-scaling** dựa trên load

---

### 📚 Tài Liệu Tham Khảo

- [Distributed Systems Concepts](https://example.com)
- [Golang Gin Framework](https://gin-gonic.com/)
- [LevelDB Documentation](https://github.com/syndtr/goleveldb)

---
