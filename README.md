# Camera Coach (web)

AI hướng dẫn canh góc chụp ảnh, chạy ngay trên điện thoại. Canh xong, bấm **Camera gốc** để chụp bằng Camera của iPhone với chất lượng đầy đủ.

- Miễn phí: chạy trên GitHub Pages.
- Không có API key: AI là MediaPipe của Google, chạy trong Safari trên máy bạn.
- Không gửi ảnh đi đâu.

## Đưa lên GitHub Pages (khoảng 5 phút)

1. Vào github.com → đăng nhập → **New repository**.
   - Tên: `camera-coach`
   - Chọn **Public** (GitHub Pages miễn phí cần repo công khai; code không có gì bí mật).
   - Bấm **Create repository**.
2. Trong repo mới, bấm **uploading an existing file**. Kéo vào **tất cả** các file và thư mục trong gói này: `index.html`, `manifest.webmanifest`, thư mục `icons`, `README.md`. Bấm **Commit changes**.
3. Vào **Settings → Pages**. Ở mục **Build and deployment**:
   - Source: **Deploy from a branch**
   - Branch: **main**, thư mục **/ (root)** → **Save**.
4. Chờ 1–2 phút, tải lại trang Settings → Pages. Link app hiện ở trên cùng, dạng `https://tên-github.github.io/camera-coach/`.

## Cài lên iPhone như một app

1. Mở link trên bằng **Safari** (không dùng app Claude hay Zalo).
2. Bấm nút **Chia sẻ** → **Thêm vào MH chính** → **Thêm**.
3. Mở app từ biểu tượng mới trên màn hình chính → **Bật camera** → cho phép **Camera** và **Chuyển động & hướng** (để làm thước cân bằng).

Lần đầu mở, app tải khoảng 10 MB mô hình AI. Những lần sau nhanh hơn.

## Cài nút Camera gốc (1 lần)

Bấm **Camera gốc** lần đầu, app hiện hướng dẫn:

1. App **Phím tắt** → **+** → Thêm tác vụ → gõ "Camera" → chọn tác vụ mở Camera. Đặt tên Shortcut là **Coach Camera**.
2. **Cài đặt → Camera** → bật **Lưới** và **Cân bằng**, để khi sang Camera gốc vẫn có mốc giữ đúng góc.
3. Chụp xong, vuốt thanh ngang dưới đáy màn hình sang phải để quay lại Camera Coach. App sẽ hỏi có muốn chấm điểm ảnh vừa chụp không.

## Sửa app sau này

Sửa file trên GitHub (bấm vào file → biểu tượng bút chì → Commit). Khoảng 1 phút sau GitHub Pages cập nhật. Trên iPhone, tắt hẳn app rồi mở lại để nhận bản mới.

## Nếu có lỗi

- **"Chưa có quyền camera"**: Cài đặt → Safari → Camera → Cho phép. Với app ở màn hình chính, iOS có thể hỏi lại quyền camera mỗi lần mở; đó là cách iOS xử lý web app.
- **"Không tải được AI nhận diện"**: kiểm tra mạng rồi mở lại. Thước cân bằng vẫn dùng được khi không có AI.
- **Hướng dẫn xoay/nghiêng bị ngược**: báo lại để đổi dấu trong code.
