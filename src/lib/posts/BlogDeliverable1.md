---
title: "Blog Deliverable 1"
date: "2025-05-30"
updated: "2025-05-30"
categories:
  - "Deliverable"
coverImage: "/images/deliverable1.jpg"
coverWidth: 16
coverHeight: 9
excerpt: Deliverable 1
---

# Ứng dụng GoLevelDB trong lưu trữ phân tán danh bạ điện thoại

## 1. Giới thiệu GoLevelDB

### Mục đích của GoLevelDB

GoLevelDB là một thư viện cơ sở dữ liệu dạng **key-value** được viết bằng ngôn ngữ Go, dựa trên LevelDB (do Google phát triển bằng C++). Mục tiêu của GoLevelDB là cung cấp một cơ sở dữ liệu **nhẹ, nhanh và dễ tích hợp**, phù hợp với các ứng dụng nhúng hoặc các hệ thống phân tán cần lưu trữ cục bộ.

### Vấn đề GoLevelDB có thể giải quyết

- Lưu trữ dữ liệu key-value cục bộ hiệu quả.
- Tối ưu tốc độ đọc/ghi tuần tự.
- Dễ dàng tích hợp vào hệ thống phân tán hoặc ứng dụng microservice.
- Thích hợp cho các ứng dụng cần hiệu năng cao nhưng không cần hệ quản trị cơ sở dữ liệu phức tạp.

### Ưu điểm

- Nhẹ, nhanh, nhúng trực tiếp không cần cài đặt thêm.
- Hỗ trợ snapshot, iterator, batch write.
- Phù hợp với ứng dụng có dữ liệu đơn giản dạng key-value.

### Nhược điểm

- Không hỗ trợ SQL hoặc truy vấn phức tạp.
- Không có giao diện quản lý người dùng.
- Cần cẩn trọng khi sử dụng snapshot, iterator để tránh rò rỉ bộ nhớ.

### So sánh với các thư viện khác

| Thư viện        | Loại                    | Ưu điểm                             | Nhược điểm                         | Phù hợp cho                     |
|------------------|-------------------------|--------------------------------------|------------------------------------|---------------------------------|
| **GoLevelDB**    | Key-Value nhúng         | Nhẹ, nhanh, dễ tích hợp              | Không hỗ trợ query nâng cao        | Lưu trữ đơn giản, hiệu năng cao |
| **BoltDB / bbolt** | Key-Value nhúng       | Giao dịch ACID, dễ dùng              | Tốc độ ghi chậm hơn LevelDB        | Dữ liệu nhỏ, cần tính nhất quán |
| **BadgerDB**     | Key-Value nhúng         | Tối ưu SSD, tốc độ cao               | Tốn RAM nếu cấu hình sai           | Cache, logs, blockchain         |
| **SQLite**       | Quan hệ (nhúng)         | Có SQL, quản lý schema tốt           | Chậm với dữ liệu lớn               | App cần quan hệ dữ liệu         |
| **Redis**        | In-memory, client-server| Tốc độ rất cao, nhiều cấu trúc dữ liệu | Phụ thuộc mạng, RAM cao            | Cache, real-time system         |

### Ứng dụng thực tế

- Ứng dụng desktop/mobile cần lưu dữ liệu cục bộ.
- Node lưu trữ trong hệ thống phân tán, P2P.
- Hệ thống danh bạ, cấu hình, log, dữ liệu trạng thái.

---

## 2. Kế hoạch bài giữa kỳ

### Tên đề tài

**Xây dựng hệ thống lưu trữ danh bạ điện thoại sử dụng cơ sở dữ liệu phân tán với GoLevelDB**

### Mục tiêu

- Ứng dụng GoLevelDB để lưu trữ danh bạ theo mô hình key-value.
- Mô phỏng hệ thống lưu trữ phân tán gồm nhiều node.
- Hỗ trợ các thao tác: thêm, xóa, cập nhật, tìm kiếm danh bạ.
- Mô phỏng phân phối dữ liệu giữa các node.

### Nội dung công việc

| Tuần   | Nội dung                                                  |
|--------|-----------------------------------------------------------|
| Tuần 1–2 | Tìm hiểu GoLevelDB và mô hình lưu trữ phân tán         |
| Tuần 3 | Thiết kế cấu trúc lưu trữ danh bạ bằng key-value         |
| Tuần 4 | Cài đặt tính năng thêm/xóa/sửa/tìm kiếm danh bạ          |
| Tuần 5 | Mô phỏng nhiều node và cơ chế phân phối dữ liệu          |
| Tuần 6 | Hoàn thiện báo cáo, kiểm thử và trình bày kết quả        |

### Kết quả mong đợi

- Ứng dụng lưu trữ danh bạ bằng GoLevelDB, hỗ trợ CRUD.
- Mô phỏng hệ thống phân tán với nhiều node lưu trữ.
- Báo cáo giữa kỳ: kiến trúc, mã nguồn, thử nghiệm.

---
