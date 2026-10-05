# Báo Cáo Bài Tập 1: Khởi Tạo Local Repository Và Cấu Hình Danh Tính

- **Khóa học:** IT209 - DevOps
- **Họ và tên:** Nguyễn Tiến Thành
- **Mã số sinh viên (MSSV):** B24DTCN283
- **Email:** thenngk6@gmail.com
- **GitHub Username:** ThanhDZsudo
- **Đường dẫn nộp bài dự kiến:** `homework/session_04/ex1/`

---

## 1. Mục Tiêu Bài Tập
- Khởi tạo thành công một Git repository trống tại thư mục làm việc cục bộ.
- Thiết lập thông tin danh tính tác giả (họ tên và email) ở cấp độ cục bộ (`--local`), không làm ảnh hưởng đến cấu hình toàn cục (`--global`).
- Tạo tệp tin mới, đưa vào vùng chuẩn bị (Staging Area) và tiến hành commit đầu tiên.
- Đọc và phân tích trạng thái thư mục làm việc (`git status`) và lịch sử commit (`git log`).

---

## 2. Các Bước Thực Hiện Chi Tiết

### Bước 1: Khởi tạo Git repository tại thư mục làm việc
Khởi tạo kho chứa cục bộ bằng lệnh `git init`:
```bash
git init
```
**Kết quả thực thi:**
```text
Initialized empty Git repository in E:/BaiTap/IT209_Devops/Session04/Ex1/.git/
```

---

### Bước 2: Cấu hình danh tính cục bộ (`--local`)
Sử dụng cờ `--local` để đảm bảo danh tính chỉ áp dụng riêng cho repository này:
```bash
# Cấu hình tên tác giả
git config --local user.name "Nguyễn Tiến Thành"

# Cấu hình email tác giả
git config --local user.email "thenngk6@gmail.com"
```

---

### Bước 3: Tạo tệp tin mới và kiểm tra trạng thái ban đầu
Tạo tệp `README.md` với nội dung báo cáo bài tập, sau đó kiểm tra trạng thái của thư mục làm việc:
```bash
git status
```
**Kết quả thực thi:**
```text
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md

nothing added to commit but untracked files present (use "git add" to track)
```
> **Phân tích:** Tệp `README.md` đang ở trạng thái `Untracked` (chưa được Git theo dõi).

---

### Bước 4: Đưa tệp tin vào vùng chuẩn bị (Staging Area)
Sử dụng lệnh `git add` để đưa `README.md` vào Staging Area chuẩn bị commit:
```bash
git add README.md
git status
```
**Kết quả thực thi `git status`:**
```text
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   README.md
```
> **Phân tích:** Tệp đã được chuyển vào mục `Changes to be committed` (Staging Area), sẵn sàng để lưu vết (commit).

---

### Bước 5: Tiến hành commit đầu tiên
Tạo commit đầu tiên với thông điệp rõ ràng:
```bash
git commit -m "Initial commit: Khoi tao du an va them tep README.md"
```

---

## 3. Kết Quả Kiểm Tra Và Bằng Chứng Thực Thi (Verification)

### 3.1. Kiểm tra cấu hình danh tính cục bộ

#### Lệnh kiểm tra tên:
```bash
git config --local user.name
```
**Output:**
```text
Nguyễn Tiến Thành
```

#### Lệnh kiểm tra email:
```bash
git config --local user.email
```
**Output:**
```text
thenngk6@gmail.com
```

#### Lệnh liệt kê toàn bộ cấu hình local (`git config --local --list`):
```bash
git config --local --list
```
**Output:**
```text
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true
user.name=Nguyễn Tiến Thành
user.email=thenngk6@gmail.com
```

---

### 3.2. Kiểm tra lịch sử commit (`git log`)

#### Lệnh `git log --oneline`:
```bash
git log --oneline
```
**Output:**
```text
fbe4d1a Initial commit: Khoi tao du an va them tep README.md
```

#### Lệnh `git log -1` (xác thực Author và Email trong commit):
```bash
git log -1
```
**Output:**
```text
commit fbe4d1a8d678ef0b4ce340ace6ca45fe5a4209ad
Author: Nguyễn Tiến Thành <thenngk6@gmail.com>
Date:   Mon Oct 5 10:36:08 2026 +0700

    Initial commit: Khoi tao du an va them tep README.md
```

---

## 4. Phân Tích Kỹ Thuật
1. **Tại sao bắt buộc phải dùng tùy chọn `--local` thay vì `--global`?**
   - Tùy chọn `--global` áp dụng cho toàn bộ các repository trên máy tính người dùng. Khi làm việc với nhiều dự án khác nhau (dự án cá nhân, dự án công ty, bài tập trường), mỗi dự án có thể yêu cầu email và tên tác giả riêng biệt.
   - Sử dụng `--local` giúp ghi đè và cô lập cấu hình danh tính chỉ trong phạm vi repository hiện tại (được lưu tại `.git/config`), tránh xung đột thông tin và không làm ảnh hưởng đến các dự án khác trên máy.
2. **Vai trò của vùng chuẩn bị (Staging Area):**
   - Staging Area (`git add`) đóng vai trò là một vùng đệm linh hoạt, cho phép lập trình viên lựa chọn chính xác những tệp tin hoặc thay đổi cụ thể cần đưa vào commit tiếp theo thay vì commit toàn bộ thư mục làm việc, giúp lịch sử commit luôn rõ ràng, sạch sẽ và có mục đích cụ thể.

---

## 5. Kết Luận
Thông qua Bài tập 1, học viên đã đạt được các kết quả sau:
- **Khởi tạo kho chứa thành công:** Đã sử dụng lệnh `git init` để tạo một Git repository cục bộ hoàn chỉnh.
- **Thiết lập danh tính chuẩn xác:** Đã cấu hình độc lập `user.name` ("Nguyễn Tiến Thành") và `user.email` ("thenngk6@gmail.com") ở cấp độ `--local`, đáp ứng đúng ràng buộc kỹ thuật của bài toán.
- **Thành thạo quy trình lưu vết cơ bản:** Hiểu rõ và thực hành đúng luồng chuyển đổi trạng thái của tệp tin từ **Working Directory** $\rightarrow$ **Staging Area** (`git add`) $\rightarrow$ **Local Repository** (`git commit`).
- **Kiểm tra và xác thực minh bạch:** Sử dụng thành thạo các lệnh kiểm tra trạng thái và lịch sử (`git status`, `git config --local --list`, `git log --oneline`, `git log -1`) để chứng minh tính toàn vẹn và chính xác của kho mã nguồn.
- **Ý nghĩa trong DevOps:** Việc cấu hình đúng danh tính và kiểm soát commit chặt chẽ là nền tảng cốt lõi giúp đảm bảo khả năng truy vết nguồn gốc mã nguồn (traceability/auditability) và tự động hóa trong các luồng CI/CD sau này.
