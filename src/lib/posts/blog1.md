---
title: "Blog 1: Giới thiệu Hệ thống phân tán"
date: "2025-05-29"
updated: "2025-05-29"
categories:
  - "distributed-systems"
  - "networking"
coverImage: "/images/blue.jpg"
coverWidth: 16
coverHeight: 9
excerpt: Bài viết giới thiệu hệ thống phân tán, các khái niệm, kiến trúc và ví dụ minh họa.
---

## Hệ thống phân tán là gì?

Hệ thống phân tán (Distributed System) là tập hợp nhiều máy tính độc lập (nodes) hoạt động cùng nhau như một hệ thống duy nhất đối với người dùng cuối. Các thành phần trong hệ thống có thể nằm trên các máy tính khác nhau, giao tiếp với nhau thông qua mạng.

## Các ứng dụng của hệ thống phân tán

- Hệ thống lưu trữ đám mây (Google Drive, Dropbox)
- Mạng xã hội (Facebook, Twitter)
- Thương mại điện tử (Amazon, Tiki)
- Dịch vụ phát trực tuyến (Netflix, YouTube)
- Ứng dụng ngân hàng, ví điện tử

## Các khái niệm chính của hệ thống phân tán

Một số đặc điểm quan trọng của hệ thống phân tán bao gồm:

### Scalability

Khả năng mở rộng hệ thống dễ dàng khi có thêm yêu cầu hoặc tải.

### Fault Tolerance

Khả năng duy trì hoạt động dù một số thành phần gặp sự cố.

### Availability

Khả năng sẵn sàng phục vụ người dùng mọi lúc.

### Transparency

Tính trong suốt - người dùng không cần biết hệ thống đang chạy trên bao nhiêu máy, ở đâu.

### Concurrency

Hệ thống hỗ trợ nhiều tiến trình hoặc người dùng truy cập cùng lúc.

### Parallelism

Thực hiện nhiều tác vụ cùng lúc để tăng hiệu suất.

### Openness

Hệ thống sử dụng các tiêu chuẩn mở và có thể tương tác với các hệ thống khác.

### Vertical Scaling

Tăng cường tài nguyên (CPU, RAM) của máy chủ hiện tại.

### Horizontal Scaling

Thêm nhiều máy chủ để chia tải công việc.

### Load Balancer

Thành phần điều phối yêu cầu người dùng đến các máy chủ khác nhau một cách cân bằng.

### Replication

Sao chép dữ liệu giữa nhiều node để tăng độ tin cậy và khả năng phục hồi.

## Ví dụ minh họa

**Ví dụ: Hệ thống Netflix**

Netflix sử dụng hệ thống phân tán để phát video cho hàng triệu người dùng.

- **Scalability**: Netflix tự động mở rộng số lượng máy chủ theo lưu lượng truy cập.
- **Fault Tolerance & Replication**: Dữ liệu video được sao chép giữa nhiều khu vực để tránh mất dữ liệu.
- **Availability**: Người dùng luôn truy cập được dịch vụ, ngay cả khi một phần hệ thống bị lỗi.
- **Load Balancer**: Điều phối yêu cầu video đến server gần nhất.
- **Transparency**: Người dùng không biết hệ thống phức tạp ra sao, chỉ thấy video được phát mượt.
- **Concurrency & Parallelism**: Hàng triệu người xem cùng lúc, các đoạn video được xử lý song song.
- **Openness**: Sử dụng nhiều công nghệ mã nguồn mở.
- **Horizontal Scaling**: Thêm nhiều server hơn thay vì chỉ nâng cấp một server duy nhất.

## Kiến trúc của hệ thống phân tán

Một số kiến trúc phổ biến trong hệ thống phân tán:

### 1. Client-Server

Máy khách gửi yêu cầu, máy chủ xử lý và phản hồi.

### 2. Peer-to-Peer (P2P)

Các node vừa là máy khách vừa là máy chủ (ví dụ: BitTorrent).

### 3. Microservices

Hệ thống chia thành nhiều dịch vụ nhỏ độc lập, mỗi dịch vụ xử lý một chức năng cụ thể.

### 4. Event-Driven Architecture

Các thành phần giao tiếp với nhau thông qua sự kiện (Kafka, RabbitMQ).

### 5. Service Mesh (mới)

Tăng cường khả năng giao tiếp giữa các microservices bằng cách sử dụng một lớp proxy chuyên dụng (ví dụ: Istio).

## Ví dụ kiến trúc

Ví dụ: Kiến trúc Microservices trong Shopee

- Mỗi chức năng như giỏ hàng, thanh toán, quản lý sản phẩm là một microservice riêng.
- Sử dụng **Load Balancer** và **Service Mesh** để đảm bảo giao tiếp hiệu quả.
- Mỗi dịch vụ có thể **scale horizontally** độc lập.
- Dữ liệu sản phẩm được **replicate** để tăng độ tin cậy.

