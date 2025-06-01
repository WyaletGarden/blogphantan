---
title: "Blog 5: Giao thức mạng và OpenMPI"
date: "2025-05-30"
updated: "2025-05-30"
categories:
  - "Network Protocols"
  - "Distributed Computing"
coverImage: "/images/b5.jpg"
coverWidth: 16
coverHeight: 9
excerpt: Tìm hiểu các giao thức mạng và lập trình phân tán với OpenMPI
---

# Phần 1: Các Giao Thức Mạng và Sự Tương Quan

## 1. Các Giao Thức Tầng Vận Chuyển

### TCP/IP (Transmission Control Protocol/Internet Protocol)
- **Mục đích**: Đảm bảo truyền dữ liệu đáng tin cậy, theo thứ tự và có kiểm tra lỗi
- **Đặc điểm**: 
  - Thiết lập kết nối trước khi truyền dữ liệu (three-way handshake)
  - Đảm bảo dữ liệu được gửi đến đúng thứ tự
  - Có cơ chế phục hồi lỗi

### UDP (User Datagram Protocol)
- **Mục đích**: Truyền dữ liệu nhanh, không cần thiết lập kết nối
- **Đặc điểm**:
  - Không đảm bảo thứ tự gói tin
  - Không có cơ chế phục hồi lỗi
  - Phù hợp cho ứng dụng streaming, gaming

## 2. Giao Thức Tầng Ứng Dụng

### HTTP (Hypertext Transfer Protocol)
- **Mục đích**: Truyền tải dữ liệu web
- **Đặc điểm**: 
  - Hoạt động trên TCP/IP
  - Mô hình client-server
  - Stateless protocol

### REST (Representational State Transfer)
- **Mục đích**: Kiến trúc phát triển API web
- **Đặc điểm**:
  - Sử dụng HTTP methods (GET, POST, PUT, DELETE)
  - Stateless
  - Dữ liệu thường ở dạng JSON/XML

### GraphQL
- **Mục đích**: Query language cho API
- **Đặc điểm**:
  - Client quyết định dữ liệu cần lấy
  - Một endpoint duy nhất
  - Giảm thiểu over-fetching và under-fetching

### SOAP (Simple Object Access Protocol)
- **Mục đích**: Protocol cho web services
- **Đặc điểm**:
  - Độc lập với giao thức truyền tải
  - Sử dụng XML
  - Có tính bảo mật cao

### AJAX (Asynchronous JavaScript and XML)
- **Mục đích**: Cập nhật trang web không cần tải lại
- **Đặc điểm**:
  - Asynchronous
  - Sử dụng XMLHttpRequest hoặc Fetch API
  - Tương tác với server mà không reload page

### RPC và gRPC
- **RPC (Remote Procedure Call)**:
  - Gọi hàm từ xa như gọi hàm local
  - Đơn giản hóa lập trình phân tán
- **gRPC**:
  - Framework RPC hiện đại của Google
  - Sử dụng Protocol Buffers
  - Hiệu năng cao, hỗ trợ streaming

## Mối Quan Hệ Giữa Các Giao Thức
- TCP/IP và UDP là nền tảng cho các giao thức tầng trên
- HTTP hoạt động trên TCP/IP
- REST và GraphQL đều có thể sử dụng HTTP
- AJAX có thể sử dụng REST hoặc GraphQL
- gRPC sử dụng HTTP/2 trên TCP/IP

# Phần 2: OpenMPI và Bài Toán Tính Số Nguyên Tố

## 1. Giới thiệu về OpenMPI

OpenMPI (Open Message Passing Interface) là một thư viện triển khai chuẩn MPI, được sử dụng rộng rãi trong tính toán song song và phân tán.

### Các tính năng chính:
- Hỗ trợ đa nền tảng
- Truyền thông điệp hiệu quả
- Quản lý tiến trình và tài nguyên
- Hỗ trợ nhiều kiểu dữ liệu

### Các hàm quan trọng:
- `MPI_Init()`: Khởi tạo môi trường MPI
- `MPI_Comm_size()`: Lấy tổng số tiến trình
- `MPI_Comm_rank()`: Lấy rank của tiến trình hiện tại
- `MPI_Send()`: Gửi dữ liệu
- `MPI_Recv()`: Nhận dữ liệu
- `MPI_Bcast()`: Broadcast dữ liệu
- `MPI_Reduce()`: Gom dữ liệu về một tiến trình
- `MPI_Finalize()`: Kết thúc môi trường MPI

## 2. Giải Pháp Tính 10,000,000 Số Nguyên Tố

### Chiến lược phân chia công việc:

1. **Phân đoạn dữ liệu**:
   - Chia khoảng số cần kiểm tra thành các đoạn nhỏ
   - Mỗi core xử lý một đoạn
   - Sử dụng Sieve of Eratosthenes cải tiến

2. **Cấu trúc chương trình**:
```c
// Pseudocode
void main() {
    MPI_Init();
    int rank, size;
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    MPI_Comm_size(MPI_COMM_WORLD, &size);

    // Tính khoảng số cho mỗi core
    long segment_size = RANGE / size;
    long start = rank * segment_size;
    long end = (rank + 1) * segment_size;

    // Áp dụng Sieve of Eratosthenes
    vector<bool> isPrime = sieveOfEratosthenes(start, end);

    // Gom kết quả về master process
    MPI_Reduce(...);

    MPI_Finalize();
}
```

3. **Tối ưu hóa**:
   - Sử dụng bit array thay vì boolean array
   - Chỉ kiểm tra đến căn bậc hai của số lớn nhất
   - Cache optimization cho Sieve algorithm
   - Load balancing động

4. **Khả năng mở rộng**:
   - Thiết kế chương trình để tự động phát hiện số core
   - Phân phối công việc dựa trên số core thực tế
   - Sử dụng dynamic scheduling để cân bằng tải

### Xử lý các trường hợp đặc biệt:

1. **Với số core khác nhau**:
   - Tự động điều chỉnh kích thước segment
   - Cân bằng tải động
   - Gộp kết quả theo thứ tự

2. **Xử lý lỗi**:
   - Kiểm tra tính hợp lệ của kết quả
   - Cơ chế backup và recovery
   - Logging cho debug

3. **Tối ưu hiệu năng**:
   - Sử dụng non-blocking communication
   - Overlap computation và communication
   - Tối thiểu hóa synchronization points
