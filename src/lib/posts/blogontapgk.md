---
title: "Ôn tập cuối kỳ"
date: "2025-05-20"
updated: "2025-05-20"
categories:
  - "distributed-systems"
  - "networking"
coverImage: "/images/eatinggrass.jpg"
coverWidth: 16
coverHeight: 9
excerpt: Bài viết chứa nội dụng câu hỏi ôn tập thì cuối kì.
---

## Câu 1 So sánh hệ thống Tập trung, Phi tập trung và Phân tán

### 1. Hệ thống Tập trung (Centralized System)

- **Đặc điểm**:  
  Tất cả xử lý và dữ liệu được tập trung tại một máy chủ chính duy nhất.

- **Ưu điểm**:  
  - Dễ quản lý và triển khai
  - Kiểm soát tập trung

- **Nhược điểm**:  
  - Dễ trở thành điểm nghẽn
  - Nếu máy chủ chính hỏng, toàn bộ hệ thống có thể ngừng hoạt động

- **Ví dụ**:  
  - Hệ thống quản lý điểm ở một trường học chỉ chạy trên một máy chủ
  - Cơ sở dữ liệu nội bộ của một cửa hàng nhỏ

---

### 2. Hệ thống Phi tập trung (Decentralized System)

- **Đặc điểm**:  
  Có nhiều nút độc lập, mỗi nút có thể tự đưa ra quyết định mà không cần thông qua một trung tâm duy nhất.

- **Ưu điểm**:  
  - Tăng khả năng chống lỗi
  - Khó bị kiểm soát/tấn công toàn bộ

- **Nhược điểm**:  
  - Đồng bộ và quản lý phức tạp
  - Có thể phát sinh xung đột dữ liệu

- **Ví dụ**:  
  - Blockchain (Bitcoin, Ethereum)
  - Hệ thống ngân hàng liên ngân hàng

---

### 3. Hệ thống Phân tán (Distributed System)

- **Đặc điểm**:  
  Gồm nhiều máy tính độc lập kết nối với nhau qua mạng và hoạt động như một hệ thống duy nhất.

- **Ưu điểm**:  
  - Hiệu suất cao
  - Dễ mở rộng
  - Chịu lỗi tốt

- **Nhược điểm**:  
  - Thiết kế và đồng bộ dữ liệu phức tạp
  - Khó kiểm tra và gỡ lỗi hơn

- **Ví dụ**:  
  - Google, Facebook, Netflix
  - Hệ thống Microservices ở Shopee, Tiki

---

## Tiêu chí phân biệt nhanh

| Tiêu chí                 | Tập trung            | Phi tập trung        | Phân tán                    |
|--------------------------|----------------------|-----------------------|------------------------------|
| Trung tâm xử lý          | Có 1 điểm trung tâm  | Nhiều điểm chính      | Không có, các node hợp tác   |
| Giao tiếp giữa các node | Không                | Có                    | Có                           |
| Cách lưu trữ dữ liệu      | Tập trung một chỗ     | Mỗi node giữ riêng     | Lưu trên nhiều node, có đồng bộ |
| Tính khả dụng cao        | Thấp nếu máy chủ lỗi  | Trung bình            | Cao                          |
| Ví dụ                    | Hệ thống nội bộ nhỏ   | Blockchain, DNS       | Netflix, Google Drive        |

---

## Tóm lại

- **Tập trung**: Đơn giản nhưng dễ sập nếu lỗi tại trung tâm.
- **Phi tập trung**: Tốt cho an ninh, khó quản lý.
- **Phân tán**: Mạnh mẽ và linh hoạt nhất, nhưng phức tạp về kỹ thuật.



## Câu 2: Các đặc tính của hệ thống phân tán

Dưới đây là những đặc điểm quan trọng thường gặp trong các hệ thống phân tán:

### 1. **Scalability** – Khả năng mở rộng

- Hệ thống có thể mở rộng dễ dàng khi số lượng người dùng, thiết bị hoặc khối lượng dữ liệu tăng lên.
- Gồm hai loại:
  - **Horizontal scaling**: Thêm nhiều máy mới.
  - **Vertical scaling**: Nâng cấp tài nguyên máy hiện tại.
- Ví dụ: Thêm nhiều máy chủ khi lưu lượng truy cập tăng.

---

### 2. **Fault Tolerance** – Khả năng chịu lỗi

- Hệ thống tiếp tục hoạt động bình thường ngay cả khi một phần nào đó gặp sự cố.
- Nhờ vào cơ chế **replication**, **checkpointing**, **failover**...
- Ví dụ: Một server bị lỗi, hệ thống tự động chuyển sang server khác.

---

### 3. **Availability** – Khả năng sẵn sàng

- Hệ thống luôn sẵn sàng phục vụ người dùng bất kể thời điểm nào.
- Có thể đạt được thông qua việc phân tán tải, có bản sao dự phòng và cân bằng tải.
- Ví dụ: Netflix luôn sẵn sàng phát video bất kể khu vực nào.

---

### 4. **Transparency** – Tính trong suốt

- Người dùng không cần biết hệ thống đang phân tán như thế nào, xử lý ở đâu.
- Các loại trong suốt gồm:
  - **Location transparency**: Không cần biết dữ liệu ở đâu.
  - **Access transparency**: Truy cập giống như hệ thống cục bộ.
  - **Replication transparency**: Không biết có bản sao dữ liệu.
  - **Failure transparency**: Hệ thống tự phục hồi khi có lỗi.

---

### 5. **Concurrency** – Tính đồng thời

- Cho phép nhiều tiến trình, người dùng truy cập và xử lý dữ liệu cùng lúc.
- Hệ thống phải đảm bảo dữ liệu không bị xung đột.

---

### 6. **Parallelism** – Tính song song

- Khả năng xử lý nhiều tác vụ đồng thời để tăng tốc độ và hiệu suất.
- Khác với concurrency ở chỗ: concurrency là "nhiều người dùng", còn parallelism là "nhiều tác vụ được xử lý cùng lúc".

---

### 7. **Openness** – Tính mở

- Hệ thống hỗ trợ các chuẩn mở, dễ tích hợp với các hệ thống khác.
- Có thể mở rộng, nâng cấp mà không cần thay đổi toàn bộ hệ thống.
- Ví dụ: Microservices trong Shopee có thể sử dụng nhiều công nghệ khác nhau.

---

## Câu 3: Vai trò và rủi ro khi nút chủ gặp sự cố

### Mục đích của nút chủ (Master Node)

- **Nút chủ (Master Node)** là thành phần quản lý trung tâm trong một số hệ thống phân tán, thường chịu trách nhiệm:
  - Phân phối công việc cho các nút con (worker nodes)
  - Theo dõi trạng thái và tài nguyên của hệ thống
  - Cập nhật metadata (như trong HDFS)
  - Điều phối truy cập hoặc đồng bộ dữ liệu

- Ví dụ:
  - Trong Hadoop HDFS: NameNode là nút chủ
  - Trong Kubernetes: Control Plane (API Server, Scheduler...) là các nút chủ

---

### Điều gì xảy ra nếu nút chủ gặp sự cố?

- **Tình huống xấu nhất**: Hệ thống mất khả năng điều phối, không thể xử lý yêu cầu mới hoặc mất metadata.
- **Giải pháp thường dùng**:
  - **Redundant Master**: Có nhiều nút chủ dự phòng (Active-Passive hoặc Active-Active)
  - **Leader Election**: Tự động chọn nút chủ mới (dùng thuật toán như Raft, Paxos)
  - **Checkpoint/Backup**: Luôn sao lưu trạng thái hệ thống

- Ví dụ:
  - HDFS sẽ dừng nếu NameNode duy nhất bị lỗi (trừ khi dùng High Availability mode).
  - Kubernetes sẽ tiếp tục hoạt động tạm thời, nhưng không thể tạo Pod mới nếu Control Plane bị lỗi.

---

## Tổng kết

| Thành phần               | Vai trò                                                | Rủi ro khi lỗi                          |
|--------------------------|---------------------------------------------------------|-----------------------------------------|
| Nút chủ (Master Node)    | Điều phối hệ thống, quản lý metadata, phân việc         | Mất điều phối, ngừng xử lý, mất trạng thái |
| Giải pháp khắc phục      | Dự phòng, bầu lại leader, backup                        | Đảm bảo tính liên tục và phục hồi       |


## Câu 4: Tại sao các máy trong mạng không gian sử dụng giao thức Gossip?

### Gossip Protocol là gì?

- Là một phương pháp giao tiếp trong hệ phân tán, trong đó mỗi nút **truyền thông tin cho một số nút ngẫu nhiên**, và các nút đó tiếp tục lan truyền thông tin tương tự.
- Giống như cách tin đồn lan truyền giữa người với người → Do đó gọi là "Gossip".

### Vì sao không gửi đến tất cả máy hoặc một nút trung tâm?

| Cách truyền tin               | Hạn chế chính |
|------------------------------|----------------|
| Gửi đến tất cả các máy (broadcast) | Tốn băng thông, không hiệu quả với hệ thống lớn |
| Gửi về một nút trung tâm       | Gây quá tải, dễ bị tấn công/lỗi tại điểm trung tâm |

### Lợi ích của Gossip Protocol

- **Scalability**: Mạng có thể mở rộng mà không tăng đáng kể độ trễ.
- **Fault Tolerance**: Không phụ thuộc vào nút trung tâm, nên hệ thống vẫn hoạt động khi một số nút bị lỗi.
- **Decentralization**: Các nút ngang hàng, dễ phân phối tải.
- **Hiệu quả**: Truyền thông tin nhanh chóng, lan rộng theo thời gian (thường là log(n) bước).

### Ứng dụng

- Cassandra, DynamoDB
- Cluster membership, đồng bộ trạng thái, phát hiện lỗi

---

## Câu 5: Các yếu tố cốt lõi của một hệ thống phân tán

1. **Multiple Independent Nodes (Nhiều nút độc lập)**  
   - Các máy tính riêng biệt kết nối qua mạng.

2. **Network Communication (Giao tiếp mạng)**  
   - Các nút cần giao tiếp qua TCP, UDP, RPC, HTTP, v.v.

3. **Concurrency (Tính đồng thời)**  
   - Nhiều tiến trình/ứng dụng chạy cùng lúc.

4. **No Shared Memory (Không chia sẻ bộ nhớ)**  
   - Mỗi nút có tài nguyên riêng, không truy cập trực tiếp bộ nhớ của nút khác.

5. **Fault Tolerance (Chịu lỗi)**  
   - Hệ thống có thể tiếp tục hoạt động khi một phần bị lỗi.

6. **Resource Sharing (Chia sẻ tài nguyên)**  
   - Các nút chia sẻ dữ liệu, dịch vụ và công cụ xử lý.

7. **Transparency (Tính trong suốt)**  
   - Người dùng không thấy sự phân tán phía sau.

8. **Scalability (Mở rộng)**  
   - Dễ dàng thêm máy mà không làm chậm hệ thống.

---

## Câu 6: Lý do sử dụng hệ thống phân tán

| Lý do                        | Giải thích |
|-----------------------------|------------|
| **Hiệu suất cao hơn**        | Xử lý song song nhiều tác vụ, giảm thời gian |
| **Tăng độ tin cậy**          | Nếu một nút hỏng, hệ thống vẫn tiếp tục hoạt động |
| **Khả năng mở rộng tốt**     | Dễ dàng mở rộng quy mô mà không thay đổi toàn bộ |
| **Tính sẵn sàng cao**        | Người dùng có thể truy cập dịch vụ mọi lúc |
| **Tiết kiệm chi phí**        | Dùng nhiều máy rẻ thay vì đầu tư một siêu máy tính |
| **Chia sẻ tài nguyên**       | Các nút chia sẻ dữ liệu, phần mềm, phần cứng |
| **Gần với người dùng hơn**   | Đặt các nút ở nhiều khu vực để giảm độ trễ |
| **Hỗ trợ tổ chức phân tán**  | Các công ty lớn có chi nhánh nhiều nơi có thể phối hợp hiệu quả |

---

