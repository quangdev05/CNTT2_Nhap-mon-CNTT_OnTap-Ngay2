# BÀI LÀM – ÔN TẬP NGÀY 2

- **Họ tên:** Phạm Duy Quang
- **Lớp:** CNTT2
- **Link repository:** https://github.com/quangdev05/CNTT2_Nhap-mon-CNTT_OnTap-Ngay2
- **Hệ điều hành (Windows/macOS):** Windows

## Bài 1. Lọc log thủ công

### Lệnh đã chạy

```shell
gc logs/access.log | Select-String "ERROR" > logs/error_report.txt
gc logs/error_report.txt
```

### 2 dòng lỗi đầu tiên trong error_report.txt

```text
2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)
```

## Bài 2. Đếm bằng pipeline

### Lệnh

```shell
gc logs/access.log | Select-String "WARNING" | Measure-Object
gc logs/payment.log | Select-String "ERROR" | Measure-Object
```

### Kết quả đếm (Windows: giá trị Count; macOS: con số in ra)

```text
WARNING trong access.log: 4

ERROR trong payment.log: 3
```

## Bài 3. Chạy script auto_warning (.ps1 hoặc .sh)

### Lệnh chạy (Windows: nếu dùng Phụ lục 2 thì ghi cả 2 lệnh)

```shell
.\auto_warning.ps1
```

### Nội dung file logs/warning_report.txt

```text
=== CANH BAO THANH TOAN ===

2025-10-18 09:19:13 [WARNING] Cong thanh toan phan hoi cham
2025-10-18 09:28:16 [WARNING] Nhieu lan nhap sai ma OTP
2025-10-18 09:43:01 [WARNING] So du vi gan bang hoc phi
2025-10-18 09:46:22 [WARNING] So du vi gan bang hoc phi
2025-10-18 09:49:43 [WARNING] So du vi gan bang hoc phi
```

## Bài 4. Báo cáo tổng hợp

### Các lệnh đã chạy

```shell
"=== TONG HOP ACCESS LOG ===" > logs/tong_hop_ngay2.txt
gc logs/access.log | Select-String "ERROR" >> logs/tong_hop_ngay2.txt
gc logs/payment.log | Select-String "WARNING" | Measure-Object | Select-Object -ExpandProperty Count >> logs/tong_hop_ngay2.txt
gc logs/tong_hop_ngay2.txt
```

### Nội dung file logs/tong_hop_ngay2.txt

```text
=== TONG HOP ACCESS LOG ===

2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:33:51 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:37:19 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:49:43 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:53:11 [ERROR] Het thoi gian cho (timeout)


5
```

## Bài 5. Câu hỏi ngắn

- **a)** Lệnh `... >` file và `... >>` file khác nhau thế nào?
  - `>` dùng để ghi nội dung vào file, nếu file đã có dữ liệu thì sẽ bị ghi đè.
  - `>>` dùng để nối nội dung mới vào cuối file, giữ nguyên nội dung cũ.
- **b)** Ở Bài 4, nếu lệnh thứ hai (nối các dòng ERROR) dùng > thay cho >>, nội dung file tong_hop_ngay2.txt sẽ thay đổi ra sao?
  - Tiêu đề === TONG HOP ACCESS LOG === sẽ bị ghi đè và mất đi, chỉ còn các dòng chứa ERROR trong file.
- **c)** Vì sao trong script nên dùng đường dẫn tương đối logs/payment.log thay vì đường dẫn tuyệt đối trên máy mình (ví dụ C:/Users/An/Desktop/...)?
  - Đường dẫn tương đối giúp script dễ chạy trên máy khác khi cấu trúc thư mục được giữ nguyên, không phụ thuộc vào tên người dùng hay vị trí thư mục trên máy.

## Tự chấm (điền sau khi có đáp án)

- **Điểm tự chấm:** 100/100
- **Lỗi mình đã mắc và cách sửa:**
