---
title: "Apache Hbase"
date: "2025-04-29"
updated: "2025-04-29"
categories:
  - "sveltekit"
  - "markdown"
coverImage: "/images/jefferson-santos-fCEJGBzAkrU-unsplash.jpg"
coverWidth: 16
coverHeight: 9
excerpt: Check out how heading links work with this starter in this post.
---

# 📚 Tổng quan về Apache HBase

Apache HBase là một **cơ sở dữ liệu phân tán, phi quan hệ (NoSQL)** được thiết kế để xử lý **dữ liệu lớn theo thời gian thực**, xây dựng trên nền tảng của **Apache Hadoop** và **HDFS**. HBase có kiến trúc tương tự như Google Bigtable.

---

## 🎯 Mục đích của HBase

- Lưu trữ và truy xuất dữ liệu lớn theo thời gian thực với hàng tỷ dòng và hàng triệu cột.
- Phù hợp cho dữ liệu **phi cấu trúc hoặc bán cấu trúc**.
- Hệ thống **phân tán** với khả năng **mở rộng ngang** dễ dàng.
- Dễ tích hợp với hệ sinh thái Hadoop như **MapReduce, Spark, Hive**.

---

## 🔍 HBase có thể giải quyết vấn đề gì?

| Vấn đề | HBase giải quyết như thế nào |
|-------|-------------------------------|
| Xử lý dữ liệu lớn | Phân tán và scale-out |
| Dữ liệu key-value lớn | Thiết kế column-oriented phù hợp |
| Truy xuất nhanh theo dòng thời gian | Hỗ trợ truy vấn real-time theo row key |
| Không cần schema cố định | Cho phép schema động, linh hoạt |
| Tích hợp big data stack | Làm việc trực tiếp với Hadoop, HDFS, Phoenix, Spark |

---

## 💪 Điểm mạnh của HBase

- Khả năng **mở rộng cực cao** theo chiều ngang.
- **Real-time read/write** với dung lượng dữ liệu cực lớn.
- Tích hợp sâu với hệ sinh thái Hadoop.
- Phù hợp cho các hệ thống log, timeline, time-series, IoT.
- **Schema linh hoạt**: mỗi hàng có thể khác cột.

---

## ⚠️ Điểm yếu của HBase

- Không hỗ trợ **truy vấn SQL gốc** (cần Apache Phoenix).
- Không tối ưu cho **JOINs**, **GROUP BY**, **truy vấn phức tạp**.
- Phụ thuộc nặng vào **thiết kế row key**.
- **Triển khai phức tạp**, khó vận hành hơn MongoDB hoặc PostgreSQL.
- **Chậm hơn Cassandra** trong một số use case streaming nhỏ.

---

## ⚔️ So sánh với các hệ thống khác

| Tiêu chí | HBase | Cassandra | MongoDB | MySQL/PostgreSQL |
|----------------------|--------------------|-------------------|-------------------|--------------------|
| Kiểu dữ liệu | Column-family | Column-family | Document (JSON) | Table (RDBMS) |
| Mở rộng | Ngang (tốt) | Ngang (rất tốt) | Ngang (tốt) | Có hạn |
| Real-time | Có (row key) | Rất tốt | Tốt | Giới hạn |
| Query linh hoạt | Không (dùng Phoenix)| Có (CQL) | Có (JSON query) | Rất linh hoạt |
| Dễ triển khai | Khó | Trung bình | Dễ | Dễ |
| Tích hợp Hadoop tốt | Rất tốt | Trung bình | Trung bình | Kém |

---

## 🌐 Các loại ứng dụng web có thể dùng HBase

### 1. Hệ thống phân tích log real-time / dashboards
- Thu thập log từ web/app/server.
- Trực quan hóa dữ liệu qua dashboard (Grafana, Kibana...).

### 2. Mạng xã hội / hệ thống feed thời gian thực
- Lưu timeline, bình luận, like, hoạt động người dùng.

### 3. Hệ thống đề xuất nội dung
- Gợi ý video, bài viết, sản phẩm dựa vào hành vi người dùng.

### 4. Ứng dụng IoT / hệ thống cảm biến
- Ghi nhận dữ liệu cảm biến thời gian thực từ hàng ngàn thiết bị.

### 5. Hệ thống tài chính / viễn thông
- Lưu trữ giao dịch, lịch sử cuộc gọi, phân tích thời gian thực.

---

## 🧰 Công nghệ thường dùng kèm HBase

| Tầng | Công nghệ |
|------|-----------|
| Frontend | React, Angular, Vue |
| Backend | Spring Boot (Java), Flask (Python), Node.js |
| Middleware | Apache Phoenix, Apache Spark, Kafka |
| Storage | HDFS (Hadoop Distributed File System) |

---

## 🌍 Trang web sử dụng HBase tiêu biểu

- **Facebook Messenger**: Lưu trữ tin nhắn theo thời gian thực (theo báo cáo học thuật từ SUNY).
- **Yahoo**, **Adobe**, **Trend Micro**: Dùng trong hệ thống phân tích dữ liệu lớn.

---