---
title: "Kế hoạch dự án"
date: "2025-04-29"
updated: "2025-04-29"
categories:
  - "Hệ thống phân tán"
  - "Distributed Systems"
coverImage: "/images/ảnh đồ án.png"
coverWidth: 16
coverHeight: 9
---

# 🗂️ KẾ HOẠCH DỰ ÁN GIỮA KỲ
## 🔖 Tên đề tài:
**Xây dựng ứng dụng web mạng xã hội thu nhỏ sử dụng Apache HBase**

---

## 🎯 Mục tiêu dự án
- Xây dựng một ứng dụng web mạng xã hội đơn giản gồm các chức năng:
- Đăng ký / đăng nhập
- Đăng bài viết (status)
- Like, comment
- Sử dụng Apache HBase làm hệ thống lưu trữ chính, khai thác khả năng xử lý dữ liệu lớn theo thời gian thực.

---

## 🔍 Bài toán cần giải quyết
- Hệ thống mạng xã hội thường xử lý dữ liệu lớn với tốc độ cao (bài viết, tương tác, hoạt động người dùng).
- Apache HBase cung cấp giải pháp lưu trữ phân tán, linh hoạt và hiệu quả cho các ứng dụng dạng time-series.

---

## 🧰 Công nghệ sử dụng

| Thành phần | Công nghệ |
|-----------------|--------------------------------------|
| Frontend | ReactJS hoặc HTML/CSS |
| Backend | Node.js hoặc Spring Boot |
| Database | Apache HBase |
| Storage layer | Hadoop HDFS |
---

## 📦 Thiết kế cơ sở dữ liệu (HBase)

| Bảng | Row Key | Cột chính | Mô tả |
|------------|-----------------------------|----------------------------|-------------------------------|
| `users` | `user_id` | name, email, joined_date | Thông tin người dùng |
| `posts` | `user_id#timestamp` | content, media | Bài viết của người dùng |
| `comments` | `post_id#comment_id` | user_id, content, time | Bình luận bài viết |
| `likes` | `post_id#user_id` | time | Người dùng like bài viết |

---

## 📅 Kế hoạch thực hiện

| Tuần | Nội dung thực hiện |
|------|--------------------------------------------------------------|
| 1 | Xác định đề tài, mục tiêu, kiến trúc tổng quát |
| 2 | Thiết kế bảng dữ liệu trong HBase |
| 3 | Cài đặt HBase, xây dựng backend API |
| 4 | Thiết kế giao diện người dùng |
| 5 | Kết nối frontend ↔ backend ↔ HBase |
| 6 | Tinh chỉnh hệ thống, chuẩn bị báo cáo & demo |

---

## ✅ Kết quả mong đợi
- Hệ thống mạng xã hội đơn giản hoạt động ổn định trên nền HBase.
- Thể hiện khả năng lưu trữ và truy xuất dữ liệu nhanh theo thời gian thực.
- Có thể mở rộng thêm tính năng như gợi ý bạn bè, thông báo, hoặc chat.

---