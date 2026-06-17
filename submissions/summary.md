# Test Summary — Báo cáo tổng hợp kiểm thử

> **Hướng dẫn**: Đây là hoạt động **Quality Assurance** — bạn đánh giá chất lượng tổng thể của phần mềm, không chỉ liệt kê lỗi.

---

# 📋 Test Summary — Báo cáo tổng hợp kiểm thử

## 1. Thông tin nhóm
- **Nhóm:** STQA Group 28   
- **Ngày báo cáo:** 17/06/2026  
- **Hệ thống kiểm thử:** https://stqa.rbc.vn — v1.0  

---

## 2. Tổng quan kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 28 |
| Pass | 21 |
| Fail | 7 |
| Blocked | 0 |
| Not Run | 0 |
| Tỷ lệ Pass | ~75% |
| Số bug phát hiện | 7 |

### Phân bổ theo nhóm chức năng
| Nhóm chức năng | TC | Pass | Fail | Bug | Đánh giá |
|----------------|----|------|------|-----|----------|
| Đăng nhập | 5 | 3 | 2 | BUG-04, BUG-02 | Trung bình |
| Quản lý user | 4 | 2 | 2 | BUG-01, BUG-06 | Trung bình |
| Quản lý sách | 4 | 4 | 0 | - | Tốt |
| Mượn/Trả sách | 5 | 5 | 0 | - | Tốt |
| Tìm kiếm | 2 | 1 | 1 | BUG-03 | Trung bình |
| Quản trị | 2 | 1 | 1 | BUG-07 | Trung bình |
| Bổ sung | 6 | 6 | 0 | - | Tốt |

### Phân bổ bug theo mức độ
| Mức độ | Số lượng | Bug IDs |
|--------|----------|---------|
| High   | 1        | BUG-02 |
| Medium | 4        | BUG-01, BUG-03, BUG-05, BUG-07 |
| Low    | 2        | BUG-04, BUG-06 |

---

## 3. Kỹ thuật thiết kế đã sử dụng
| Kỹ thuật | Áp dụng cho REQ nào | Số TC sử dụng | Giải thích |
|----------|---------------------|---------------|------------|
| EP (Equivalence Partitioning) | REQ-01 → REQ-07 | 22 | Chia lớp dữ liệu hợp lệ/không hợp lệ để kiểm thử |
| BVA (Boundary Value Analysis) | REQ-01, REQ-04 | 4 | Kiểm thử mật khẩu sai, mượn quá giới hạn, hết số lượng |
| DT (Decision Table) | REQ-02, REQ-03 | 2 | Kiểm thử xóa user/sách đang mượn |

---

## 4. Phân tích chất lượng phần mềm

### 4.1 Điểm mạnh
- Chức năng thêm/xóa sách hoạt động đúng.  
- Đăng nhập với tài khoản hợp lệ vào dashboard thành công.  
- Tìm kiếm sách không tồn tại trả về thông báo chính xác.  

### 4.2 Điểm yếu
- Cho phép thành viên hết hạn mượn sách (BUG-02).  
- Validation email chưa chặt chẽ (BUG-01).  
- Hiển thị số sách mượn không chính xác (BUG-05).  
- Giao diện ngôn ngữ không đồng bộ (BUG-07).  

---

## 5. Đề xuất ưu tiên sửa lỗi
| Thứ tự | Bug | Mức độ | Lý do ưu tiên |
|--------|-----|--------|---------------|
| 1 | BUG-02 | High | Ảnh hưởng trực tiếp đến logic nghiệp vụ mượn sách |
| 2 | BUG-05 | Medium | Sai dữ liệu số lượng sách mượn |
| 3 | BUG-01 | Medium | Vi phạm quy tắc nhập liệu |
| 4 | BUG-03 | Medium | Tìm kiếm không chính xác |
| 5 | BUG-07 | Medium | Giao diện ngôn ngữ không đồng bộ |
| 6 | BUG-04 | Low | Hiển thị trạng thái không đồng bộ |
| 7 | BUG-06 | Low | Thiếu thông báo khi đổi trạng thái |

---

## 6. Kết luận
Hệ thống đạt **75% test case Pass**, nhưng chưa sẵn sàng phát hành vì tồn tại bug nghiêm trọng (BUG-02). Cần khắc phục bug High và Medium trước khi triển khai chính thức.

---

## 7. Bài học rút ra
- Thiết kế test case đa dạng (EP, BVA, DT) giúp phát hiện nhiều lỗi logic.  
- Minh chứng hình ảnh giúp báo cáo thuyết phục và dễ kiểm tra.  
- Việc đối chiếu Bug ↔ TC ↔ REQ giúp quản lý chất lượng chặt chẽ.

---

## 8. Khai báo sử dụng AI (Tùy chọn)

> Nếu nhóm có sử dụng công cụ AI (ChatGPT, Copilot, Gemini...), hãy ghi rõ bên dưới. Khai báo trung thực **không ảnh hưởng điểm** — đây là kỹ năng minh bạch trong nghề.

| Công cụ AI | Dùng cho phần nào | Bạn đã kiểm tra/chỉnh sửa thế nào |
|------------|-------------------|-----------------------------------|
| | | |
