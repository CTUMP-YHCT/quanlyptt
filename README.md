# PTT Châm cứu – Mượn phòng & Báo cáo 6S-3R

Trang web tĩnh (GitHub Pages) + backend Google Apps Script/Google Sheet cho Phòng thực tập Châm cứu, BM Châm cứu – Xoa bóp – Dưỡng sinh, Khoa YHCT, ĐH Y Dược Cần Thơ. Áp dụng theo QT-BMCC-TS-01 (biểu mẫu BM-11, BM-12).

## Cấu trúc
- `index.html` – trang chính: mượn phòng, lịch, chấm 6S-3R, tổng hợp, xuất CSV, mã QR
- `poster.html` – poster A4 có QR tự sinh theo địa chỉ trang
- `apps-script/Code.gs` – backend lưu dữ liệu vào Google Sheet

## Bước 1. Tạo backend (Google Sheet + Apps Script)
1. Tạo Google Sheet mới, đặt tên “PTT Cham cuu – Du lieu”.
2. Menu **Tiện ích mở rộng → Apps Script**, xóa code mẫu, dán toàn bộ `apps-script/Code.gs`, lưu.
3. Chọn hàm `setup` → **Chạy** → cấp quyền. Sheet sẽ có 3 trang: `bookings`, `reports6s`, `settings`.
4. **Cài đặt dự án (bánh răng) → Thuộc tính tập lệnh**:
   - `ADMIN_PIN` = mã quản trị (đổi ngay giá trị mặc định)
   - `STAFF_PIN` = mã GV gửi báo cáo 6S (không bắt buộc)
5. **Triển khai → Tùy chọn triển khai mới → Ứng dụng web**:
   - Thực thi dưới dạng: **Tôi**
   - Người có quyền truy cập: **Bất kỳ ai**
   - Sao chép URL dạng `https://script.google.com/macros/s/.../exec`

## Bước 2. Cấu hình trang
Mở `index.html`, thay dòng:
```js
const API_URL = "PASTE_APPS_SCRIPT_WEB_APP_URL_HERE";
```
bằng URL Web App ở bước 1.

## Bước 3. Đưa lên GitHub Pages
1. Tạo repository **public**, ví dụ `ptt-chamcuu`.
2. **Add file → Upload files**: kéo thả `index.html`, `poster.html`, `README.md`, thư mục `apps-script`.
3. **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, Branch = `main` / `(root)` → Save.
4. Sau 1–2 phút, trang có địa chỉ: `https://<tên-github>.github.io/ptt-chamcuu/`
5. Mở `…/ptt-chamcuu/poster.html` để in poster QR.

## Phân quyền
| Việc | Ai làm được |
|---|---|
| Xem lịch, trạng thái phòng, báo cáo 6S | Mọi người có link |
| Gửi đăng ký mượn phòng | Mọi người có link |
| Hủy / trả phòng | Người đăng ký (trên cùng thiết bị) hoặc quản trị |
| Duyệt / từ chối, cấu hình phòng, xem SĐT, họ tên | Quản trị (nhập `ADMIN_PIN`) |
| Gửi báo cáo 6S-3R | Mọi người, hoặc chỉ người có `STAFF_PIN` nếu đặt |

## Lưu ý
- Link là công khai: không đưa thông tin nhạy cảm vào ghi chú. Họ tên và SĐT người mượn chỉ hiện cho quản trị và chính người đăng ký.
- Khi sửa `Code.gs`: **Triển khai → Quản lý triển khai → Chỉnh sửa → Phiên bản mới** để URL giữ nguyên.
- Dữ liệu gốc nằm ở Google Sheet; có thể lọc, lập báo cáo trực tiếp trên Sheet.
