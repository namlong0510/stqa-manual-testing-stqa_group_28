# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Group 28 -->` |
| **Ngày tạo** | `<!-- DD/MM/YYYY -->` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Email có tồn tại trong DB? | Có | `librarian@library.com` | Đăng nhập thành công |
| | Không | `noone@email.com` | Thông báo lỗi |
| Mật khẩu có đúng? | Đúng | `admin123` | Đăng nhập thành công |
| | Sai | `wrongpass` | Thông báo lỗi |
| Ô nhập có rỗng? | Không rỗng | (giá trị bất kỳ) | Xử lý bình thường |
| | Rỗng | `""` | Thông báo "Vui lòng nhập..." |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| `<!-- Nhóm tự điền -->` | | | |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

### REQ-01: Login

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | Technique |
|-------|----------------|--------------|-------|------------|-----------------|-----------|
| TC01 | Successful login | Active account | Enter email + password | librarian@library.com / admin123 | Dashboard displayed | EP |
| TC02 | Wrong password | Active account | Enter email + wrong password | librarian@library.com / wrongpass | Error “Wrong password” | BVA |
| TC03 | Non-existent email | Not in DB | Enter email | noone@email.com | Error message | EP |
| TC04 | Suspended account | User status Suspended | Login | lu.le@email.com / password123 | Error “Account suspended” | EP |
| TC05 | Expired account | User status Expired | Login | binh.pham@email.com / password123 | Error “Account expired” | EP |

---

### REQ-02: User Management

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | Technique |
|-------|----------------|--------------|-------|------------|-----------------|-----------|
| TC06 | Add valid user | Admin login | Go to user management, enter new info | New email, Active role | User added successfully | EP |
| TC07 | Add duplicate email | Email exists | Enter duplicate email | librarian@library.com | Error message | EP |
| TC08 | Edit user role | User exists | Change role | Active → Librarian | Role updated | EP |
| TC09 | Delete user with borrowed books | User has borrowed books | Delete user | MEM004 | Error message | DT |

---

### REQ-03: Book Management

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | Technique |
|-------|----------------|--------------|-------|------------|-----------------|-----------|
| TC10 | Add new book | Admin login | Enter book info | New ISBN | Book added successfully | EP |
| TC11 | Add duplicate ISBN | ISBN exists | Enter duplicate ISBN | BOOK001 | Error message | EP |
| TC12 | Edit book info | Book exists | Change quantity | BOOK002 | Update successful | EP |
| TC13 | Delete borrowed book | Book is borrowed | Delete book | BOOK003 | Error message | DT |

---

### REQ-04: Borrow Books

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | Technique |
|-------|----------------|--------------|-------|------------|-----------------|-----------|
| TC14 | Borrow available book | Active user | Select available book, click “Borrow” | BOOK001 | Success | EP |
| TC15 | Borrow out-of-stock book | Quantity = 0 | Select book | BOOK005 | Error message | BVA |
| TC16 | Borrow beyond limit | User already borrowed 3 books | Borrow more | MEM006 | Error “Limit exceeded” | BVA |

---

### REQ-05: Return Books

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | Technique |
|-------|----------------|--------------|-------|------------|-----------------|-----------|
| TC17 | Return on time | User has borrowed books | Return before due date | BOOK001 | Status “Returned” | EP |
| TC18 | Return overdue | User has overdue books | Return book | BOOK002 | Status “Overdue”, fee applied | EP |

---

### REQ-06: Search Books

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | Technique |
|-------|----------------|--------------|-------|------------|-----------------|-----------|
| TC19 | Valid search | DB has “Flutter” | Enter keyword | “Flutter” | Show results | EP |
| TC20 | Invalid search | DB has none | Enter keyword | “XYZ123” | Show “No results” | EP |

---

### REQ-07: Roles & Admin Page

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | Technique |
|-------|----------------|--------------|-------|------------|-----------------|-----------|
| TC21 | Access admin page as Librarian | Login librarian@library.com | Access admin page | Role Librarian | Success | EP |
| TC22 | Access admin page as Active user | Login ba.nguyen@email.com | Access admin page | Role Active | Denied, error “Insufficient rights” | EP |
| TC23 | Change role Active → Librarian | Admin login | Edit user role | MEM006 → Librarian | Role updated | EP |
| TC24 | Invalid role assignment | Admin login | Enter invalid role | Role = “SuperUser” | Error message | BVA |

---

### REQ-08: Reports & Statistics

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | Technique |
|-------|----------------|--------------|-------|------------|-----------------|-----------|
| TC25 | View borrowed books report | Admin login | Go to reports | Select “Borrowed books” | Correct statistics | EP |
| TC26 | View active users report | Admin login | Go to reports | Select “Active users” | Correct statistics | EP |
| TC27 | Export report to CSV | Admin login | Go to reports, export CSV | Report “Borrowed books” | CSV file created correctly | EP |
| TC28 | Export empty report | Admin login | Go to reports, export CSV | Report “Expired books” | Empty CSV, error “No data” | DT |

---

## Summary

| Function Group              | #TC | REQ Covered     | IDM Techniques |
|-----------------------------|-----|-----------------|----------------|
| Login                       | 5   | REQ-01          | EP, BVA        |
| User Management             | 4   | REQ-02          | EP, DT         |
| Book Management             | 4   | REQ-03          | EP, DT         |
| Borrow Books                | 3   | REQ-04, REQ-05  | EP, BVA        |
| Return Books                | 2   | REQ-05          | EP, BVA        |
| Search Books                | 2   | REQ-06          | EP             |
| Roles & Admin Page          | 4   | REQ-07          | EP, BVA        |
| Reports & Statistics        | 4   | REQ-08          | EP, DT         |
| **Total**                   | **28** | REQ-01 → REQ-08 | EP, BVA, DT   |
