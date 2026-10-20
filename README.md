# 20/10 · Room 3D — TrLinh

Website chúc mừng Ngày Phụ nữ Việt Nam 20/10 với căn phòng Three.js, album ảnh, lời chúc, quà tặng và biểu mẫu gửi lời nhắn đến **TrLinh**.

- **Mã nguồn:** [Luongtranlinh111/luongtranlinh20-10](https://github.com/Luongtranlinh111/luongtranlinh20-10)
- **GitHub Pages:** [luongtranlinh111.github.io/luongtranlinh20-10](https://luongtranlinh111.github.io/luongtranlinh20-10/)
- **Email nhận lời nhắn:** `luongtranlinh9114@gmail.com`

Địa chỉ website hoạt động sau khi GitHub Pages được bật và lượt triển khai hoàn thành. Xem trạng thái trong tab **Actions** của repository.

## Tính năng

- Màn mở đầu và căn phòng có bốn điểm khám phá: phong thư, album, gương và hộp quà.
- Bức thư có hiệu ứng khi cuộn và các hộp lời chúc có thể mở.
- Album tám ảnh: chuyển bằng nút, vuốt hoặc phím mũi tên; chạm ảnh để phóng to.
- Các lời nhắc, sáu món quà và phần kết mở khóa sau khi khám phá đủ bốn góc phòng.
- Trang phong thư đặc biệt tại `bonus.html`, ký tên **TrLinh ♡**.
- Nhạc nền bật/tắt bằng nút **BẬT NHẠC**.
- Biểu mẫu gồm tên, email, lời nhắn và đánh giá 1–5, gửi qua FormSubmit.

Website dùng HTML, CSS và JavaScript thuần; không có backend riêng, không cần `npm install` hay bước build. Three.js được lưu sẵn trong `js/vendor/three/`. Khi WebGL2 không khả dụng, giao diện phòng CSS vẫn cho phép truy cập nội dung.

## Chạy trên máy tính

### VS Code và Live Server

1. Tải hoặc clone repository về máy.
2. Mở thư mục dự án bằng VS Code.
3. Cài extension **Live Server** nếu chưa có.
4. Nhấp phải `index.html` → **Open with Live Server**.

### Python

Cần Git để clone và Python 3 để chạy máy chủ. Mở PowerShell hoặc terminal:

```powershell
git clone https://github.com/Luongtranlinh111/luongtranlinh20-10.git
cd luongtranlinh20-10
python -m http.server 8765 --bind 127.0.0.1
```

Mở [http://127.0.0.1:8765/](http://127.0.0.1:8765/). Nếu Windows dùng lệnh `py`, thay lệnh cuối bằng:

```powershell
py -m http.server 8765 --bind 127.0.0.1
```

Dừng máy chủ bằng `Ctrl+C`. Nếu đã có mã nguồn, chỉ cần mở terminal tại thư mục chứa `index.html` và chạy lệnh máy chủ.

**Hãy dùng địa chỉ HTTP khi chạy thử.** Mở trực tiếp bằng `file://` sẽ dùng phòng CSS dự phòng; module 3D và biểu mẫu gửi email cần HTTP/HTTPS. FormSubmit và Google Fonts cần Internet; nhạc có thể chỉ phát sau khi người xem tương tác.

## Cấu trúc mã nguồn

```text
.
├── .github/workflows/pages.yml  # Tự động xuất bản GitHub Pages
├── .nojekyll                    # Phục vụ tài nguyên tĩnh
├── index.html                  # Trang chính và các khu vực nội dung
├── bonus.html                  # Trang phong thư đặc biệt
├── piano.mp3                   # Nhạc nền đang dùng
├── css/
│   ├── global.css              # Giao diện và hiệu ứng chung
│   ├── pages.css               # Các trang nội dung
│   ├── room3d.css              # Giao diện căn phòng
│   ├── world3d.css             # Bề mặt và chiều sâu
│   └── bonus3d.css             # Trang phong thư đặc biệt
├── js/
│   ├── config.js              # Email và đường dẫn kết nối
│   ├── app.js                 # Điều hướng, tiến trình, nhạc, hộp thoại
│   ├── pages.js               # Thư, album, quà và biểu mẫu email
│   ├── room3d-loader.js        # Nạp cảnh 3D và xử lý dự phòng
│   ├── room3d.js               # Three.js, ánh sáng, camera, tương tác
│   ├── bonus.js               # Mở/đóng phong thư đặc biệt
│   └── vendor/three/           # Three.js và giấy phép MIT
├── assets/photos/              # memory-01.jpg ... memory-08.jpg
├── image/                      # Tài nguyên hình ảnh cũ
├── dist/                       # Bản HTML cũ
└── js/dist/                    # Bản cấu hình biên dịch cũ
```

**Bản triển khai dùng các file gốc, `css/`, `js/` và `assets/photos/`.** Workflow chỉ đóng gói các tài nguyên được liệt kê trong `pages.yml`; `dist/`, `js/dist/`, `image/` và `assets/ambient.wav` không được dùng cho bản Room 3D đang xuất bản.

## Tùy chỉnh nội dung

### Email và liên kết cuối trang

Chỉnh `js/config.js`:

```javascript
window.SITE_CONFIG = {
  connectUrl: "bonus.html?v=20261011-rose-ui",
  ownerEmail: "luongtranlinh9114@gmail.com",
  formSubmitEndpoint: "https://formsubmit.co/ajax/luongtranlinh9114@gmail.com"
};
```

- `connectUrl`: trang mở khi chọn **Mở trang kết nối**; có thể thay bằng URL HTTPS.
- `ownerEmail`: email hiển thị trên giao diện.
- `formSubmitEndpoint`: địa chỉ nhận dữ liệu; cập nhật cùng `ownerEmail` khi đổi hộp thư.

Email trong `index.html` là nội dung hiển thị ban đầu trước khi JavaScript cập nhật, nên đổi cả dòng `.mail-address` khi đổi email. Các đoạn nhắc tên, tiêu đề email và placeholder nằm trong `index.html`; thông báo sau khi gửi nằm trong `js/pages.js`; chữ ký phong thư nằm trong `bonus.html`.

### Ảnh trong album

Thay tám ảnh trong `assets/photos/` và giữ tên `memory-01.jpg` đến `memory-08.jpg`. Ảnh cần thực sự có định dạng JPEG; đổi đuôi `.png` thành `.jpg` không chuyển đổi định dạng ảnh. Nên nén ảnh trước khi đưa lên để tải nhanh trên điện thoại.

Đổi chú thích, thứ tự hoặc số lượng ảnh tại mảng **`MEMORYS`** trong `js/pages.js`. Nếu thay đường dẫn ảnh đầu tiên, sửa cả thẻ ảnh ban đầu trong `index.html`. Nếu dùng PNG/WebP hoặc thư mục khác, cập nhật đường dẫn trong mã **và** bước **Prepare current website** của workflow để những ảnh đó được đưa lên Pages.

### Lời chúc và tên hiển thị

| Nội dung cần sửa | Vị trí |
| --- | --- |
| Tiêu đề tab, màn mở đầu, ngày tháng, lời nhắc, quà và biểu mẫu | `index.html` |
| Các đoạn thư dài | Mảng `LETTER_TEXT` trong `js/pages.js` |
| Lời nhắn trong các hộp nhỏ | Mảng `CHIBI_MESSAGES` trong `js/pages.js` |
| Chú thích ảnh | Mảng `MEMORYS` trong `js/pages.js` |
| Phong thư đặc biệt và chữ ký | `bonus.html` |
| Màu sắc, phông chữ, khoảng cách, hiệu ứng | Các file trong `css/` |
| Đồ vật, ánh sáng và camera 3D | `js/room3d.js` |

Giữ file ở mã hóa **UTF-8** để tiếng Việt hiển thị đúng. Không cần chỉnh các bản cũ trong `dist/` để thay đổi website hiện tại.

### Nhạc nền

Thay `piano.mp3` ở thư mục gốc bằng MP3 của bạn và giữ tên. Nếu đổi tên hoặc định dạng, sửa thẻ `<source>` bên trong `#bgMusic` của `index.html`, đồng thời cập nhật danh sách sao chép trong workflow. `assets/ambient.wav` là tài nguyên cũ, không phải nhạc đang phát.

## Kích hoạt và kiểm tra gửi email

Biểu mẫu gửi dữ liệu từ trình duyệt đến **[FormSubmit](https://formsubmit.co/)** bằng AJAX. Email người gửi được dùng làm địa chỉ trả lời (`Reply-To`); thông tin biểu mẫu được xử lý qua dịch vụ này.

1. Triển khai website hoặc mở bằng Live Server/Python HTTP server.
2. Đi đến phần gửi lời nhắn, nhập tên, email hợp lệ, nội dung và đánh giá.
3. Gửi một lời nhắn thử.
4. Mở hộp thư **`luongtranlinh9114@gmail.com`**, kiểm tra cả Spam và thư kích hoạt của FormSubmit nếu được yêu cầu.
5. Làm theo liên kết kích hoạt trong thư, rồi gửi lại lời nhắn thử từ website.
6. Xác nhận thư đến đúng hộp thư; dùng **Reply** để kiểm tra địa chỉ người gửi.

Việc cập nhật mã nguồn không tự xác nhận quyền sở hữu hộp thư. Người có quyền truy cập Gmail cần thực hiện kích hoạt nếu FormSubmit yêu cầu. Thông báo gửi thành công trên website thể hiện phản hồi từ dịch vụ; hãy kiểm tra hộp thư thực tế để xác nhận thư đã đến. Không cần và không được đưa mật khẩu Gmail vào mã nguồn.

## Triển khai lên GitHub Pages

Workflow tại `.github/workflows/pages.yml` chạy khi push lên nhánh **`main`** hoặc được chạy thủ công.

### Thiết lập lần đầu

1. Đảm bảo mã nguồn và workflow nằm trên nhánh `main` của [repository](https://github.com/Luongtranlinh111/luongtranlinh20-10).
2. Mở **Settings → Pages → Build and deployment**.
3. Ở **Source**, chọn **GitHub Actions**.
4. Mở **Actions → Deploy website to GitHub Pages**.
5. Nếu chưa có lượt chạy, chọn **Run workflow**, chọn `main`, rồi chạy.
6. Đợi job thành công và mở URL trong environment **github-pages** hoặc tab **Settings → Pages**.

URL theo cấu hình mặc định là **[https://luongtranlinh111.github.io/luongtranlinh20-10/](https://luongtranlinh111.github.io/luongtranlinh20-10/)**. Đây là project site nên đường dẫn có `/luongtranlinh20-10/`. Nếu cấu hình tên miền riêng, dùng địa chỉ GitHub hiển thị trong phần Pages.

Workflow tạo thư mục tạm `_site/`, sao chép website, tải artifact và triển khai bằng GitHub Pages. Không cần build trên máy. Giữ tên thư mục, chữ hoa/thường và đường dẫn tương đối vì GitHub Pages phân biệt chữ hoa/thường.

### Cập nhật những lần sau

Trong thư mục clone từ repository đích:

```powershell
git switch main
git pull --ff-only origin main
```

Sửa nội dung rồi xem thay đổi trước khi đưa lên:

```powershell
git status
git diff
git add index.html bonus.html js/config.js js/pages.js README.md
git commit -m "Update TrLinh website"
git push origin main
```

Lệnh `git add` là ví dụ cho những file nội dung thường sửa. Nếu đổi ảnh, nhạc, CSS hoặc workflow, thêm đúng các file đó vào lệnh. Sau mỗi lần push, theo dõi tab **Actions** đến khi triển khai thành công. Git cần đăng nhập tài khoản có quyền ghi; không lưu token truy cập trong file dự án.

## Kiểm tra trước khi chia sẻ

- Mở qua HTTP/HTTPS; xác nhận phòng tải được hoặc hiển thị giao diện dự phòng.
- Mở đủ bốn góc phòng, kiểm tra tiến trình và phần kết.
- Chuyển qua tám ảnh, thử phóng to, đóng ảnh và kiểm tra trên màn hình điện thoại.
- Bật/tắt nhạc; mở trang kết nối và phong thư đặc biệt.
- Kiểm tra tên **TrLinh** và email **`luongtranlinh9114@gmail.com`**.
- Khi cần kiểm tra gửi email thật, gửi lời nhắn thử và xác nhận trong Gmail sau khi kích hoạt FormSubmit.

## Xử lý lỗi thường gặp

| Hiện tượng | Cách xử lý |
| --- | --- |
| Pages báo 404 | Kiểm tra workflow thành công, Source là GitHub Actions và URL có `/luongtranlinh20-10/`; lần xuất bản đầu có thể cần thêm thời gian. |
| Push xong nhưng nội dung chưa đổi | Xem lượt chạy mới nhất, xác nhận đã push nhánh `main`, tải lại không dùng cache (`Ctrl+F5`). Nếu cần, đổi giá trị `?v=` của file đã cập nhật trong HTML. |
| Phòng 3D không xuất hiện | Dùng HTTP/HTTPS, cập nhật trình duyệt, kiểm tra WebGL2/tăng tốc phần cứng và Console; giao diện dự phòng vẫn dùng được. |
| Không thấy ảnh hoặc nhạc trên Pages | Kiểm tra tên, chữ hoa/thường, đường dẫn và danh sách sao chép trong workflow; file chỉ có ở máy sẽ không xuất hiện trên website. |
| Nhạc không tự phát | Nhấn BẬT NHẠC; trình duyệt thường yêu cầu thao tác người dùng trước khi phát âm thanh. |
| Form không gửi khi mở file trực tiếp | Mở bằng Live Server hoặc Python HTTP server. |
| Form lỗi hoặc không nhận thư | Kiểm tra mạng, endpoint trong `js/config.js`, thư kích hoạt/Spam rồi thử lại; lỗi mạng có thể hết thời gian chờ sau 20 giây. |
| Action bị từ chối triển khai | Kiểm tra Pages đã bật, Actions được phép chạy và environment `github-pages` có yêu cầu phê duyệt hay giới hạn nhánh không. |

## Thư viện

Three.js được lưu kèm dự án; giữ `three.module.js`, `three.core.js` và giấy phép MIT trong `js/vendor/three/` khi phân phối. Thông tin phiên bản và nguồn tải nằm trong `js/vendor/three/README.md`.

