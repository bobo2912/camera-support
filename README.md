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
3. **Cho khung ảnh khớp nhau**: nút nhỏ ở góc dưới bên trái khung ngắm (4:3 / 16:9 / 1:1) phải trùng với tỉ lệ đang chọn trong app Camera. Nếu Camera để 16:9 mà app để 4:3, phần hai bên sẽ bị cắt mất. Giữ zoom 1× ở cả hai app.
4. Chụp xong, vuốt thanh ngang dưới đáy màn hình sang phải để quay lại Camera Coach. Muốn chấm điểm ảnh vừa chụp, bấm nút ảnh nhỏ bên trái nút chụp.

## AI đọc khung cảnh thế nào

Ngoài việc tìm người và đồ vật, app đọc thêm khung cảnh (không cần mô hình AI, chạy trên ảnh thu nhỏ):

- **Hướng nhìn của người**: người nghiêng mặt sang trái thì đặt ở đường 1/3 bên phải, chừa khoảng trống trước mặt, và ngược lại.
- **Nền rối bên nào**: nếu một bên người nhiều đồ đạc, chi tiết hơn hẳn bên kia, app đẩy người về phía đó để khung chứa nhiều phần nền gọn hơn.
- **Đường chân trời / đường ngang chính** (mép biển, mép tường với sàn…): không để nằm giữa khung, không để cắt ngang đầu, cổ người. Trời nhiều mây, hoàng hôn thì cho trời chiếm 2/3; trời trơn thì cho cảnh bên dưới chiếm 2/3.
- Đồ vật nhỏ trong một không gian rộng được coi là khung cảnh (đặt ở giao điểm 1/3), không bị kéo vào giữa như chụp sản phẩm.

## Không phải cấp quyền camera mỗi lần

Từ bản 1.2, nếu bạn đã cho phép camera một lần, app mở thẳng vào camera, không cần bấm "Bật camera".
Quyền camera do iOS quản lý. Để iOS không hỏi lại:

- **Cài đặt → Ứng dụng → Safari → Camera → Cho phép** (iOS cũ hơn: Cài đặt → Safari → Camera).
- Hoặc mở link app trong Safari → nút **aA** trên thanh địa chỉ → **Cài đặt trang web** → **Camera: Cho phép**.

Thước cân bằng dùng cảm biến nghiêng. Nếu iOS cần hỏi lại quyền này, chỉ cần chạm vào màn hình một lần.

## Kiểu chụp (recipes.json)

"Gu" bố cục của AI nằm trong file `recipes.json`. Mỗi kiểu chụp là một mục:

```json
{
  "id": "nguoi-toan-than-chan-dai",
  "scene": "person",
  "name": "Toàn thân, chân dài",
  "source": "Video TikTok của @...",
  "howto": "Hạ máy ngang hông, ngửa nhẹ lên...",
  "auto": false,
  "subject": { "x": "center", "y": 0.95, "anchor": "feet" },
  "size": { "metric": "body", "min": 0.7, "max": 0.93 },
  "camera": { "down": [95, 112], "raise": "Hạ máy xuống ngang hông rồi ngửa lên" },
  "hint": "Giữ máy thấp, chân chạm sát mép dưới",
  "pose": "Bạn đứng thẳng, dồn trọng tâm sang một chân"
}
```

| Trường | Ý nghĩa |
|---|---|
| `scene` | `person` (người), `landscape` (phong cảnh), `food` (đồ ăn), `product` (sản phẩm) |
| `auto` | `false` = chỉ dùng khi bạn chọn tay. Bỏ trống = AI được tự chọn |
| `subject.x` | Chủ thể nằm ở đâu theo chiều ngang: `"thirds"` (AI tự chọn đường 1/3 trái hay phải theo hướng nhìn của người và độ rối của nền), `"nearest-third"` (đường 1/3 gần nhất), `"left-third"`, `"right-third"`, `"center"` hoặc số 0–1 |
| `subject.y` | Theo chiều dọc: `"top-third"`, `"bottom-third"`, `"thirds"`, `"center"` hoặc số 0–1 (0 = mép trên) |
| `subject.anchor` | Điểm nào của chủ thể đặt vào vị trí trên: `face` (mặt), `feet` (bàn chân), `center` (giữa) |
| `size` | Độ lớn chủ thể: `metric` là `face` (bề ngang mặt / bề ngang khung), `body` (chiều cao người / chiều cao khung) hoặc `area` (diện tích); `min`, `max` từ 0 đến 1 |
| `camera.down` | Khoảng góc máy cho phép, độ: 0 = chĩa thẳng xuống đất, 90 = cầm thẳng, trên 90 = ngửa lên |
| `camera.raise` / `camera.lower` | Câu nhắc khi cần ngửa lên / chúc xuống |
| `hint` | Câu hiện khi đã đạt chuẩn |
| `pose` | Câu đọc cho người được chụp khi đạt chuẩn (chế độ Chỉnh người) |
| `weight` | Mức quan trọng của vị trí, 1 là bình thường |

Sửa `recipes.json` trên GitHub, chờ 1–2 phút, tắt hẳn app rồi mở lại. Cài đặt → cuối trang ghi số kiểu chụp đang có.

## Pin và nhiệt độ

- Hình xem trước khoảng 1280×960 ở 24 hình/giây (ảnh đẹp đã có Camera gốc lo). AI chạy khoảng 4 lần mỗi giây, thưa hơn khi máy đứng yên, khi đã canh chuẩn hoặc khi máy xử lý chậm.
- Đang chụp người thì nhận diện đồ vật và phân loại cảnh chỉ chạy vài giây một lần.
- **Tự tạm dừng** (mặc định bật): máy nằm yên 30 giây hoặc 3 phút không chạm thì app nghỉ camera và AI. Chạm để tiếp tục, không phải cấp quyền lại.
- **Tiết kiệm pin** (Cài đặt): hình xem trước 960×720 ở 15 hình/giây, AI chạy khoảng 2 lần mỗi giây.
- Góc dưới bên phải màn hình có số đo tải AI, ví dụ `AI 18 ms · 5.2/s`: số mili giây AI mất cho mỗi lần phân tích và số lần mỗi giây. Chữ chuyển cam khi trên 40 ms, đỏ khi trên 80 ms (máy đang quá tải, nên bật Tiết kiệm pin). Tắt được trong Cài đặt.

## Cập nhật phiên bản mới

App tự kiểm tra file `version.json` trên GitHub mỗi lần mở, mỗi khi quay lại app và 10 phút một lần. Khi có bản mới, trên cùng màn hình hiện nút **"Cập nhật 1.x"**. Bấm vào là app tải bản mới và mở lại. Trong Cài đặt có nút **Kiểm tra cập nhật**.

Khi phát hành bản mới, luôn tải lên **cả hai**: `index.html` (trong đó có `APP_VERSION`) và `version.json` (cùng số phiên bản). Nếu chỉ tải `version.json` mà quên `index.html`, nút Cập nhật sẽ hiện mãi.

## Sửa app sau này

Sửa file trên GitHub (bấm vào file → biểu tượng bút chì → Commit). Khoảng 1 phút sau GitHub Pages cập nhật. Trên iPhone, tắt hẳn app rồi mở lại để nhận bản mới.

## Nếu có lỗi

- **"Chưa có quyền camera"**: Cài đặt → Safari → Camera → Cho phép. Với app ở màn hình chính, iOS có thể hỏi lại quyền camera mỗi lần mở; đó là cách iOS xử lý web app.
- **"Không tải được AI nhận diện"**: kiểm tra mạng rồi mở lại. Thước cân bằng vẫn dùng được khi không có AI.
- **Hướng dẫn xoay/nghiêng bị ngược**: báo lại để đổi dấu trong code.
