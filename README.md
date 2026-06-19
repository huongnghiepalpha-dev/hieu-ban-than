# Hướng dẫn Deploy — HNA Hiểu Mình Web App
**Phiên bản:** 1.0 | **Ngày:** 2026

---

## Cấu trúc file

```
hna_hieu_minh_gas/
├── Code.gs       ← Backend GAS (lưu Sheet, gửi email)
├── Index.html    ← Toàn bộ app frontend (trắc nghiệm + PDF)
└── README_DEPLOY.md  ← File này
```

---

## Bước 1 — Tạo Google Apps Script project

1. Mở **[script.google.com](https://script.google.com)**
2. Nhấn **+ New project**
3. Đặt tên: `HNA_HieuMinh`

---

## Bước 2 — Tạo file Code.gs

1. File mặc định tên `Code.gs` đã có sẵn
2. **Xóa toàn bộ nội dung** và **paste** nội dung từ `Code.gs` vào
3. Nhấn **Ctrl+S** để lưu

---

## Bước 3 — Tạo file Index.html

1. Nhấn dấu **+** bên cạnh "Files" → chọn **HTML**
2. Đặt tên: `Index` *(không cần .html, GAS tự thêm)*
3. **Xóa toàn bộ nội dung** và **paste** nội dung từ `Index.html` vào
4. Nhấn **Ctrl+S** để lưu

---

## Bước 4 — Khởi tạo Google Sheet (chạy 1 lần)

1. Trong GAS editor, chọn function **`initializeSheet`** từ dropdown
2. Nhấn **▶ Run**
3. Lần đầu chạy sẽ yêu cầu cấp quyền → nhấn **Review permissions**
   - Chọn tài khoản Google của HNA
   - Nhấn **Advanced** → **Go to HNA_HieuMinh (unsafe)** → **Allow**
4. Sau khi chạy xong, mở **Execution log** để xem URL của Google Sheet vừa tạo

> **Lưu ý:** Sheet tự động tạo trong Drive tài khoản đang chạy Script. Nếu muốn lưu vào Sheet có sẵn, sao chép Sheet ID và điền vào `CONFIG.SHEET_ID` trong `Code.gs`.

---

## Bước 5 — Deploy Web App

1. Nhấn **Deploy** (góc trên phải) → **New deployment**
2. Nhấn biểu tượng ⚙️ cạnh "Select type" → chọn **Web app**
3. Điền thông tin:
   - **Description:** `HNA Hieu Minh v1.0`
   - **Execute as:** `Me (huongnghiepalpha@gmail.com)`
   - **Who has access:** `Anyone` *(để học sinh truy cập không cần đăng nhập)*
4. Nhấn **Deploy**
5. Nhấn **Authorize access** nếu được hỏi
6. **Sao chép Web app URL** — đây là link chia sẻ cho học sinh

> URL có dạng:
> `https://script.google.com/macros/s/AKfycby.../exec`

---

## Bước 6 — Kiểm tra

1. Mở Web app URL trên trình duyệt → App hiển thị bình thường
2. Làm thử 1 bài hoàn chỉnh → kiểm tra:
   - Kết quả hiển thị đúng
   - Google Sheet có dòng dữ liệu mới
   - Email gửi đến địa chỉ học sinh nhập
   - Email thông báo gửi đến `huongnghiepalpha@gmail.com`
3. Thử nút **Tải kết quả PDF** → file PDF tải về máy

---

## Bước 7 — Cập nhật app (sau khi sửa code)

Mỗi khi sửa `Code.gs` hoặc `Index.html`:

1. Nhấn **Deploy** → **Manage deployments**
2. Nhấn ✏️ **Edit** bên cạnh deployment hiện tại
3. Chọn **Version:** `New version`
4. Nhấn **Deploy**

> ⚠️ Không tạo deployment mới — chỉ cập nhật deployment cũ để giữ nguyên URL.

---

## Cấu hình tùy chỉnh (trong Code.gs)

```javascript
var CONFIG = {
  SHEET_ID: '',              // Để trống = tự tạo. Điền ID nếu muốn lưu vào Sheet sẵn có
  SHEET_NAME: 'KetQua_HieuMinh',  // Tên tab trong Google Sheet
  SEND_EMAIL_STUDENT: true,  // true = gửi email xác nhận cho học sinh
  SEND_EMAIL_HNA: true,      // true = gửi thông báo lead về HNA
  HNA_EMAIL: 'huongnghiepalpha@gmail.com',  // Email nhận thông báo
};
```

---

## Nhúng vào website huongnghiepalpha.vn (Bước 4 — tương lai)

Thêm đoạn HTML sau vào trang bất kỳ trên website:

```html
<iframe
  src="https://script.google.com/macros/s/AKfycby.../exec"
  width="100%"
  height="800px"
  frameborder="0"
  style="border-radius:12px; box-shadow:0 4px 20px rgba(0,0,0,0.08);"
  title="Trắc nghiệm Hiểu Mình - Hướng Nghiệp Alpha">
</iframe>
```

> Thay `AKfycby...` bằng Web app URL thực tế từ Bước 5.

---

## Cột dữ liệu trong Google Sheet

| # | Tên cột | Ví dụ |
|---|---------|-------|
| A | Thời gian | 18/06/2026 14:30:00 |
| B | Họ và tên | Nguyễn Văn An |
| C | Lớp/Khối | Lớp 11 |
| D | Trường | THPT Biên Hòa |
| E | Tỉnh/TP | Đồng Nai |
| F | Email | an@gmail.com |
| G | SĐT phụ huynh | 0912345678 |
| H | Mã Holland | SE |
| I | Holland Top 1 | Xã hội |
| J | Holland Top 2 | Doanh nhân |
| K–P | Điểm R/I/A/S/E/C | 18/12/22/28/25/14 |
| Q | MI Top 1 | Tương quan |
| R | MI Top 2 | Ngôn ngữ |
| S–Z | Điểm 8 loại MI | 20/18/15/... |
| AA | Gợi ý nghề nghiệp | Quản lý giáo dục\|Nhân sự HR\|... |
| AB | Session ID | HNA_1750000000000 |

---

## Xử lý lỗi thường gặp

| Lỗi | Nguyên nhân | Cách xử lý |
|-----|-------------|------------|
| App hiện trang trắng | Deploy chưa đúng | Kiểm tra lại Bước 5 |
| Không lưu được Sheet | Chưa cấp quyền Drive | Chạy lại `initializeSheet` và cấp quyền |
| Không gửi được email | Chưa cấp quyền Gmail | Chạy thử `sendEmailHNA` với dữ liệu mẫu |
| PDF không tải được | Lỗi jsPDF CDN | Kiểm tra kết nối internet |
| Cập nhật code không có hiệu lực | Quên tạo version mới | Xem Bước 7 |

---

## Hỗ trợ kỹ thuật

Hotline HNA: **096 937 4411**
Email: huongnghiepalpha@gmail.com
