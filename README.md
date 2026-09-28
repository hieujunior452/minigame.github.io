# Đuổi Hình Bắt Chữ — Thấu Hiểu Tài Chính Cá Nhân

Mini game web đơn trang: người chơi nhìn một hình minh họa, bấm **Gợi Ý** nếu bí, **Hiện Đáp Án** để đối chiếu, rồi **Câu Tiếp Theo** để đi hết 12 câu. Viết bằng HTML/CSS/JavaScript thuần, không framework, không bước build.

**Demo:** https://hieujunior452.github.io/minigame.github.io/

---

## Tóm tắt nhanh

| Thông tin | Chi tiết |
|---|---|
| Loại dự án | Mini game web đơn trang (single-page) |
| Vai trò | DEV toàn bộ — thiết kế giao diện, viết mã, triển khai |
| Quy mô mã nguồn | 1 file HTML 193 dòng (HTML + CSS + JS nội tuyến) |
| Nội dung | 12 câu hỏi về tài chính cá nhân, kèm ảnh + đáp án + gợi ý |
| Nền tảng | HTML5 + CSS3 + JavaScript ES6+ thuần, không framework |
| Hiệu ứng nền | tsParticles — 70 hạt vàng rơi xuống |
| Tài nguyên ngoài | 3 CDN (tsParticles, Font Awesome, Google Fonts) → cần Internet |
| Deploy | GitHub Pages (project site), branch `main` |

---

## Chức năng chính

| Tính năng | Mô tả | Nơi thực hiện |
|---|---|---|
| Nạp câu hỏi | Cập nhật `Câu N / 12`, đổi ảnh, reset đáp án và gợi ý về trạng thái chờ | `index.html:170-175` (`loadQuestion`) |
| Gợi ý | Chèn gợi ý vào khung vàng kèm tiền tố 💡 | `index.html:177-179` (`showHint`) |
| Hiện đáp án | Hiện đáp án màu vàng `#ffd700` trong vùng đáp án | `index.html:181-183` (`showAnswer`) |
| Câu tiếp theo | `current = (current + 1) % questions.length` → câu 12 quay về câu 1 | `index.html:185-188` (`nextQuestion`) |
| Số câu | Tự cập nhật theo `questions.length`, không hardcode | `index.html:171` |
| Hạt nền | 70 hạt vàng, kích thước 2–5, tốc độ 1.2, rơi từ trên xuống | `index.html:144-151` |

### Luồng hoạt động

```
trang tải → loadQuestion()                    (index.html:190)
              ↓
   render "Câu N / 12" + ảnh  ·  reset đáp án / gợi ý
              ↓
   [Gợi Ý]  → showHint()    ghi #hint,   không đổi trạng thái
   [Đáp Án]  → showAnswer()  ghi #answer, không đổi trạng thái
   [Tiếp]    → nextQuestion() → current = (current+1) % questions.length → loadQuestion()
```

Hai nút đầu thuần "đọc", chỉ nút cuối mới dịch chuyển `current` — người chơi xem gợi ý bao nhiêu lần cũng không bị nhảy câu.

### Bộ 12 câu hỏi

| # | Đáp án | Gợi ý (như trong mã nguồn) |
|---|---|---|
| 1 | Ghi chép kiến thức | Thầy cô hay nhắc phải chuẩn bị bút giấy để… |
| 2 | Niềm tin về tiền | Điều đầu tiên của sự thịnh vượng |
| 3 | Ba niềm tin hạn chế | Tiền xấu, tiền tội lỗi, tiền gây rắc rối |
| 4 | Tiền Đỏ | Tiền từ cờ bạc, lòng tham, bất an |
| 5 | Tiền Xanh | Tiền từ lao động chân chính, mang lại hạnh phúc |
| 6 | Hai vị thần tài lộc | Cha mẹ là… trong gia đình |
| 7 | Lòng hiếu thảo | Điều giúp thu hút tiền bạc và may mắn |
| 8 | Lòng biết ơn | Khi biến mất thì lãnh thổ cũng biến mất |
| 9 | Dòng chảy thịnh vượng | Bị tắc khi keo kiệt |
| 10 | Gieo nhân gặt quả | Cho đi trước khi nhận (Hào phóng) |
| 11 | Hào phóng / Cho đi | Rockefeller cho 60%, Gates cho 95% |
| 12 | Hiếu thảo với cha mẹ | Thần tượng bóng đá mà cô trang rất thích |

---

## Công nghệ sử dụng

| Công nghệ | Nơi thể hiện | Vai trò |
|---|---|---|
| HTML5 | `index.html:1-5`, `123-141` | `<!DOCTYPE html>`, `lang="vi"`, meta viewport; bố cục dựng bằng `<div>` kết hợp phần tử `<button>`, `<img>` |
| CSS3 | `index.html:11-116` | Inline `<style>`: flexbox, `linear-gradient` nền, gradient chữ (`-webkit-background-clip: text`), `object-fit`, `box-shadow`, `text-shadow`, `border-radius`, `transition` |
| JavaScript ES6+ | `index.html:143-191` | Inline `<script>`: `const` / `let`, template literal, DOM `getElementById` + `textContent` / `innerHTML`, xử lý sự kiện `onclick` |
| tsParticles 2 | `index.html:8`, `144-151` | Hiệu ứng hạt vàng rơi (CDN jsDelivr) |
| Font Awesome 6.6.0 | `index.html:9` | Icon `fa-coins`, `fa-lightbulb`, `fa-eye`, `fa-arrow-right` (CDN cdnjs) |
| Google Fonts | `index.html:12` | Playfair Display (700, 900) cho tiêu đề; Roboto (400, 500, 700) cho nội dung |
| GitHub Pages | — | Host tĩnh miễn phí, project site, branch `main` |

> Không framework JS, không package manager, không bước build, không test, không CI.

### Quyết định thiết kế

| Quyết định | Lý do | Nơi thể hiện |
|---|---|---|
| Web thuần, không framework | Tải nhanh, deploy tĩnh trực tiếp lên GitHub Pages, không cần pipeline build | toàn `index.html` |
| Khai báo câu hỏi dạng mảng object | Thêm câu chỉ cần thêm 1 phần tử `{ image, answer, hint }`, không sửa logic | `index.html:153-166` |
| `current = (current + 1) % questions.length` | Chỉ cần một biến trạng thái, tự quay vòng, không cần mảng trạng thái | `index.html:186` |
| tsParticles 70 hạt vàng, hướng `bottom` | Tạo chủ đề "mưa tiền" hợp tài chính, chi phí một thẻ `<script>` | `index.html:8`, `144-151` |
| Ảnh dùng `object-fit: contain`, `max-height: 360px` | Ảnh nguồn khác nhau về tỉ lệ, vẫn vừa khung ở màn hình hẹp | `index.html:71-77` |
| `innerHTML` cho gợi ý / đáp án | Dữ liệu hardcode trong mã, không có input người dùng nên không phát sinh rủi ro XSS | `index.html:178`, `182` |

---

## Cấu trúc thư mục

```
minigame.github.io/
├── index.html          # 193 dòng — bản đang hoạt động (deploy tại GitHub Pages)
├── images/             # 12 ảnh: 1–11.png + 12.webp — tổng ~25.7 MB
│                       # PNG nặng 1.5–3.1 MB/ảnh; 8.png trùng nội dung 10.png
│                       # 12.webp chỉ ~80 KB — duy nhất đã nén
└── minigame/           # Bản trùng, đang hỏng (xem mục "Lưu ý kỹ thuật")
    ├── index.html      # 241 dòng
    └── images/         # 12 ảnh y hệt thư mục images/ (cùng md5) — ~25.7 MB
```

Chưa có `LICENSE`, `package.json`, `.gitignore` hay cấu hình CI. *(Dung lượng ảnh đo ngày 28/09/2026.)*

---

## Cài đặt và chạy

**Yêu cầu:** trình duyệt hiện đại (Chrome / Firefox / Edge / Safari) và kết nối Internet để tải 3 CDN.

```bash
git clone https://github.com/hieujunior452/minigame.github.io.git
cd minigame.github.io
```

**Cách 1 — mở trực tiếp (đơn giản nhất):** mở file `index.html` bằng trình duyệt. Bản này dùng đường dẫn ảnh tương đối (`images/1.png`) nên chạy được cả với giao thức `file://`.

**Cách 2 — chạy local server:**

```bash
python3 -m http.server 8000
# Mở trình duyệt tại http://localhost:8000
```

**Cách 3 — GitHub Pages:** vào **Settings → Pages** → chọn `Deploy from a branch`, branch `main`, thư mục `/ (root)`.

> Repo tên `minigame.github.io` nhưng thuộc tài khoản `hieujunior452` (không phải user site) nên đây là **project site**; URL dạng `https://<user>.github.io/minigame.github.io/`.

---

## Giao diện

<!-- [CHÈN ẢNH 1 — Màn hình câu 1, chưa bấm nút] -->
<!-- [CHÈN ẢNH 2 — Màn hình sau khi bấm "Gợi Ý"] -->
<!-- [CHÈN ẢNH 3 — Màn hình sau khi bấm "Hiện Đáp Án"] -->
<!-- [CHÈN ẢNH 4 — Ảnh chụp trên mobile (CẦN KIỂM TRA trước khi chèn)] -->
<!-- Chèn bằng: ![Mô tả ảnh](docs/screenshots/ten-anh.png) — nên chụp rộng ~720px -->

---

## Lưu ý kỹ thuật

**Đã hoàn thiện:** vòng chơi 12 câu khép kín, quay vòng vô hạn, reset trạng thái đúng sau mỗi câu; 3 nút phân biệt màu; đường dẫn ảnh tương đối nên hoạt động đúng trên subpath của Pages.

**Điểm cần cải thiện** (rà soát trực tiếp từ mã nguồn):

| Vấn đề | Mức độ | Chi tiết | Hướng xử lý |
|---|---|---|---|
| Bản `minigame/` trùng lặp và hỏng | Trung bình | `minigame/index.html` dùng đường dẫn tuyệt đối `"/images/1.png"` → trên project site resolve thành `https://hieujunior452.github.io/images/1.png` và trả về **404**; câu 12 trỏ `"/images/12.png"` trong khi file thực tế là `12.webp`. Ảnh cũng bị nhân đôi (~25.7 MB) | Xóa toàn bộ thư mục `minigame/` |
| Ảnh chưa nén | Trung bình | 11 file PNG 1.5–3.1 MB, tổng ~25.7 MB; `12.webp` chỉ ~80 KB | Chuyển toàn bộ sang WebP/AVIF |
| Ảnh trùng nội dung | Thấp | `images/8.png` và `images/10.png` cùng md5 (`cef4b246…`) → câu 8 và 10 dùng chung một tấm ảnh | Kiểm tra lại nội dung câu 8 |
| Bố cục cứng trên màn hình thấp | Thấp | `body` đặt `height: 100vh` + `overflow: hidden` (`index.html:20-21`), ảnh `max-height: 360px` cố định (`index.html:73`) → nội dung có thể bị cắt | Cho phép cuộn, bỏ `max-height` cố định |
| Placeholder còn sót | Thấp | `index.html:129` vẫn trỏ `via.placeholder.com` (bị `loadQuestion()` ghi đè ngay nên không hiển thị) | Xóa cho sạch |
| Chưa có test / CI | Thấp | Không có test tự động | Thêm smoke test kiểm tra link ảnh |

**Chưa làm:** điểm số, lưu tiến trình bằng `localStorage`, phím tắt bàn phím, chuyển cảnh, kiểm tra đáp án do người chơi nhập.

> `[CẦN KIỂM TRA]` Giao diện mới dựa trên viewport meta + flexbox + `max-width` — chưa kiểm thử trên thiết bị thật. Cần test mobile/tablet trước khi chèn ảnh chụp màn hình vào mục *Giao diện*.

---

## Tác giả

**Nguyễn Ngọc Hiếu**

- GitHub: [@hieujunior452](https://github.com/hieujunior452)
- Dự án cá nhân, đảm nhận toàn bộ vai trò DEV: thiết kế giao diện, viết mã nguồn, chuẩn bị nội dung và triển khai.
