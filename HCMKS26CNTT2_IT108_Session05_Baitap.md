# (Bài tập tổng hợp) Giao Diện Dòng Lệnh Terminal Cơ Bản
## **Phần 1 –** CLI vs GUI và cấu trúc câu lệnh
1. ***Cho câu lệnh PowerShell: `ls -Force C:\Windows\Logs`. Xác định đâu là **Command**, đâu là **Options/Flags**, đâu là **Argument**.***
-   Command: `ls`
-   Options/Flags: `-Force`
-   Argument: `C:\Windows\Logs`
2.  ***Project `quan-ly-sinh-vien` sau khi hoàn thành sẽ được đưa lên một **máy chủ Cloud** để chạy thử. Giải thích vì sao nhóm **bắt buộc phải dùng Terminal (PowerShell/SSH)** thay vì giao diện đồ họa để làm việc với máy chủ đó, dựa trên 1 trong 3 lý do đã học.***
   Trả lời:  Máy chủ Cloud thường được quản lý từ xa qua SSH. Terminal giúp chạy lệnh nhanh, quản trị hệ thống và tự động hóa công việc mà không cần giao diện đồ họa.
## **Phần 2 –** Điều hướng hệ thống file
3.  ***Từ vị trí hiện tại ở mục 3b (`C:\Users\student\Desktop`), sau khi thư mục `quan-ly-sinh-vien` đã được tạo ngay tại đây, viết lệnh **Relative Path** để di chuyển vào bên trong thư mục đó.***
    Trả lời : `cd .\quan-ly-sinh-vien`
4.  ***Viết **Absolute Path** đầy đủ, chính xác tới file `main.py` trong cấu trúc project ở mục 3a (theo chuẩn đường dẫn Windows).***
    Trả lời: `C:\Users\student\Desktop\quan-ly-sinh-vien\src\main.py`
5.  ***Bạn đang đứng trong thư mục `src\`. Viết **một lệnh PowerShell duy nhất** (không dùng `cd` trước) để xem toàn bộ nội dung — **kể cả file ẩn** — của thư mục `data\` (cùng cấp, nằm trong thư mục cha).***
    Trả lời: `ls ..\data -Force`
        

## **Phần 3 –** Thao tác file và thư mục

6. ***Viết lệnh PowerShell tạo cùng lúc 2 thư mục con `src` và `data` bên trong `quan-ly-sinh-vien` (thư mục `quan-ly-sinh-vien` **chưa tồn tại**).***
      ` New-Item -Path ".\quan-ly-sinh-vien\src", ".\quan-ly-sinh-vien\data" -ItemType Directory`
7.  ***Viết lệnh PowerShell tạo 3 file rỗng `main.py`, `utils.py` và `README.md` trong **cùng một dòng lệnh**.***
    `New-Item -Path "src\main.py", "src\utils.py", "README.md" -ItemType File`
8.  ***Bạn lỡ đặt sai tên thư mục gốc thành `quan-ly-sv` thay vì `quan-ly-sinh-vien`.***
    -   Viết lệnh PowerShell để **đổi tên lại cho đúng**.
      `Rename-Item -Path ".\quan-ly-sv" -NewName "quan-ly-sinh-vien"`
    -   Viết thêm một lệnh để **sao lưu toàn bộ** thư mục project (đã đổi tên) thành bản backup `backup-quan-ly-sinh-vien`. _Chú ý:_ đây là copy cả thư mục kèm nội dung con — cần đúng **cờ đệ quy** của PowerShell.
        `Copy-Item -Path ".\quan-ly-sinh-vien" -Destination ".\backup-quan-ly-sinh-vien" -Recurse`

## Phần 4 – Xử lý lỗi Terminal
9.  ***Dựa vào **Log lỗi số 2** (mục 3d), chẩn đoán: đây có khả năng là lỗi gì trong **3 nguyên nhân** đã học? Đề xuất cách dùng phím **Tab** để kiểm tra nhanh nguyên nhân.***
   - Log lỗi số 2 – `Cannot find path`
   -   Nguyên nhân: Gõ sai tên thư mục `scr` thay vì `src`.
   -   Giải pháp : Dùng phím `Tab` để tự động hoàn thành tên thư mục, hoặc gõ: `cd .\src`
10.  ***Dựa vào **Log lỗi số 3** (mục 3e), chẩn đoán nguyên nhân (tương ứng với lỗi nào đã học trên Windows?) và nêu cách khắc phục theo đúng hướng dẫn Lesson 04.***
 - Log lỗi số 3 – `Access is denied`
-   Nguyên nhân: Người dùng không có quyền truy cập hoặc thực thi file script.
-   Giải pháp : Kiểm tra quyền truy cập file `setup.ps1` và thuộc tính bảo mật. Nếu file đáng tin cậy nhưng bị Windows chặn, kiểm tra `Unblock-File` trước khi chạy lại. Không nên tự động chạy bằng quyền Administrator khi chưa rõ nguyên nhân.
11.  ***Dựa vào **Log lỗi số 1** (mục 3c), chẩn đoán vì sao PowerShell đưa ra cảnh báo này, và viết **"đơn thuốc"** — lệnh PowerShell đúng, dùng cờ phù hợp — để xóa thành công thư mục `old-version` mà **không bị hỏi xác nhận**.***
 - Log lỗi số 1 – Cảnh báo khi xóa thư mục
-   Nguyên nhân: Thư mục `old-version` có chứa file hoặc thư mục con nhưng lệnh chưa có tham số `-Recurse`.
-   Giải pháp : Dùng `-Recurse` để xóa cả thư mục và nội dung bên trong, `-Force` để xử lý các mục bị ẩn hoặc chỉ đọc; thêm `-Confirm:$false` để không hỏi xác nhận.
12.  ***Áp dụng đúng **Quy trình 3 bước đọc log lỗi chuẩn Developer** (đọc từ dưới lên → bắt từ khóa lỗi → kiểm tra ngữ cảnh/vị trí hiện tại) để phân tích **Log lỗi số 4** (mục 3f). Chỉ rõ:***

| Bước | Câu trả lời |
| :--- | :--- |
| (a) Dòng chứa thông điệp lỗi trực tiếp nhất | `FileNotFoundError: [Errno 2] No such file or directory: 'data/input.csv'` |
| (b) Từ khóa lỗi (Error Keyword) | `FileNotFoundError` |
|(c)  Điều cần kiểm tra tiếp | Chương trình đang chạy từ thư mục `src`, nên đường dẫn tương đối `data/input.csv` được tìm thành `src/data/input.csv`. Cần kiểm tra lại đường dẫn và sửa thành `../data/input.csv` hoặc `../data/input.csv` theo cách biểu diễn đường dẫn phù hợp trong code Python. |
