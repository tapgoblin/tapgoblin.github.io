# tapgoblin.github.io — hướng dẫn cập nhật trang

## Nơi đặt trang

- **Trang chính thức:** https://tapgoblin.github.io — repo `tapgoblin/tapgoblin.github.io` (public, bắt buộc vì gói Free của GitHub Pages). Remote `origin` của thư mục này trỏ vào repo đó; sửa xong thì push lên `origin main`.
- **Repo cũ `Dong2VS/Dong2VS.github.io`** (remote `old-dong2vs`) không còn cập nhật. Giữ lại vì các trang privacy `dong2vs.github.io/<game>-privacy-policy/` và `app-ads.txt` cũ vẫn dùng địa chỉ đó. Đừng xoá.
- `app-ads.txt` cũng có trong repo này. Nếu trang web nhà phát triển trong Play Console đổi sang `tapgoblin.github.io` thì AdMob đọc file này.

Trang giới thiệu game của **DragonsFunny** (thương hiệu kênh: **Tap Goblin**). Người xem đến từ YouTube/TikTok bấm link để xem game và tải về. Trang là **một file tĩnh** [index.html](index.html), song ngữ EN/VI, không dùng framework.

Đọc file này trước khi sửa trang. Đừng bịa link: chỉ điền URL mà chủ dự án đã gửi hoặc đã xác minh.

## Cấu trúc

| Đường dẫn | Vai trò |
|---|---|
| `index.html` | Toàn bộ trang: CSS, HTML, JS |
| `app-ads.txt` | Xác minh AdMob. **Không sửa, không xoá.** |
| `assets/<game>.png` | Icon game, 256×256 |
| `assets/feature-<game>.jpg` | Ảnh feature graphic, 800×390 |
| `assets/tap-goblin.png` | Logo trang + favicon, 256×256, **nền trắng** (không dùng PNG trong suốt vì bị hiện nền đen) |
| `assets/tap-goblin-banner.jpg` | Banner ở đầu trang |

Trang privacy của từng game **không nằm trong repo này** và **không hiển thị trên trang** (chủ dự án đã bỏ link Privacy). Mỗi game có repo GitHub Pages riêng, dạng `https://dong2vs.github.io/<game>-privacy-policy/`; các URL này vẫn sống và là URL khai trong Google Play Console. Đừng xoá các repo đó.

Nguồn thiết kế/brand: thư mục `../Channel` (`tap_goblin_brand_guide.md`, `Design/`, `LaunchKit/`, `Images/`). Tên game, mô tả, package Android nằm trong project của từng game (`../LightWeave`, `../OddlyPairs`, `../FireflyTrails`, ...).

## Thông tin hiện có

| Game | Tên hiển thị | Trạng thái | Google Play |
|---|---|---|---|
| Connect Lights | Connect Lights: Wire Puzzle | Đã ra mắt | `com.dong2vs.lightweave` |
| Chroma Clear | Chroma Clear: Color Puzzle | Đã ra mắt | `com.chromaclear.game` |
| Firefly Trails | Firefly Trails: Forest Puzzle | Đã ra mắt | `com.dong2vs.fireflytrails` |
| Oddly Pairs | Oddly Pairs: Animal Match | **Sắp ra mắt** (chưa có trên Play) | dự kiến `com.dragonsfunny.oddlypairs`, chưa xác nhận |

- Link Play: `https://play.google.com/store/apps/details?id=<package>`
- Trang tất cả game trên Play (dùng ở mục Get in touch): `https://play.google.com/store/search?q=pub%3ADragons%20Funny&c=apps`
- YouTube: `https://www.youtube.com/channel/UCQCr_eS3s8Op_49FAAporsg` (handle `@playtapgoblin`)
- Email: dragonsfunny85@gmail.com
- Tên nhà phát triển trên Google Play: **Dragons Funny**. Trên trang viết **DragonsFunny**.
- Thứ tự thẻ game hiện tại (chủ dự án chọn): Oddly Pairs → Connect Lights → Firefly Trails → Chroma Clear.

## Việc thường gặp

### 1. Chủ dự án gửi link iOS (App Store)

Mỗi thẻ game có sẵn một nút App Store đang ẩn, ngay sau nút Google Play:

```html
<!-- iOS: add the App Store href and remove "hidden" once the game is live -->
<a class="btn dl" hidden aria-label="Download on the App Store" title="App Store">…App Store</a>
```

Với game có link: thêm `href="<link App Store>" rel="noopener"` và xoá thuộc tính `hidden`. Game nào chưa có link thì để nguyên ẩn.

Nếu có link trang nhà phát triển trên App Store, làm tương tự ở mục **Get in touch**: dòng `<li hidden>` có chữ "Our games on the App Store" → thêm `href`, xoá `hidden`.

### 2. Thêm game mới

Sao chép nguyên một thẻ `<article class="card">` trong `<div class="games">` rồi sửa:

1. Đặt icon vào `assets/<game>.png` (256×256) và feature graphic vào `assets/feature-<game>.jpg` (800×390).
2. `style="--accent:#RRGGBB"`: màu nhấn của game.
3. Nhãn trạng thái: `<p class="tag">` là **Available now / Đã ra mắt**; `<p class="tag soon">` là **Coming soon / Sắp ra mắt**.
4. Tên game `<h3>`; mô tả trong `<p class="desc">` **có cả `lang="en"` và `lang="vi"`**. Mô tả tự cắt 2 dòng và có nút "… more", không cần xử lý thêm.
5. Nút tải:
   - Đã lên Play: dùng nút `<a class="btn dl" href="https://play.google.com/store/apps/details?id=…">` (icon `#i-play`, chữ Google Play). Giữ nút iOS ẩn như mục 1.
   - Chưa lên Play: dùng `<span class="btn soon">Coming soon / Sắp ra mắt</span>`. Khi lên Play thì đổi thành nút `btn dl`, đổi nhãn sang Available now.
6. Không thêm link Privacy vào thẻ. Game mới vẫn cần trang privacy riêng (repo `<game>-privacy-policy`) để khai với store.
7. Số thẻ: lưới 4 cột trên desktop (`.games`). Từ 5 game trở lên nó tự xuống hàng; nếu muốn đổi bố cục thì chỉnh `grid-template-columns`.
8. Cập nhật số game trong `<title>`, `<meta name="description">` và bảng ở trên nếu cần.

Khi một game từ "Coming soon" lên Play: đổi tag, thay nút, cập nhật bảng trong file này.

### 3. Thêm hoặc bật kênh mạng xã hội

Mục **Get in touch** là danh sách `<ul class="contact">`. Mỗi dòng phải có **icon + chữ + link** (dòng có khung, mũi tên ↗ và hiệu ứng rê chuột là do CSS `.contact a`).

- Đang ẩn (`<li hidden>`, chưa có link): **TikTok**, **Instagram**, **App Store**. Có link thì thêm `href` + `rel="noopener"` và xoá `hidden`.
- Kênh mới: thêm một `<li>` mới, và nếu chưa có icon thì thêm `<symbol id="i-<tên>">` vào khối SVG sprite ở đầu `<body>`, rồi dùng `<svg class="ico" aria-hidden="true"><use href="#i-<tên>"/></svg>`. Icon phải theo màu và hình của nền tảng. Icon hiện có: `i-play`, `i-appstore`, `i-youtube`, `i-tiktok`, `i-instagram`, `i-mail`. Các icon này do mình vẽ tay, chưa phải logo chính thức.
- Nhớ ghi link mới vào mục "Thông tin hiện có" ở trên.

## Quy tắc khi sửa

- **Song ngữ:** mọi chữ hiển thị đều bọc `<span lang="en">…</span><span lang="vi">…</span>`. Tên riêng, email, tên nền tảng (Google Play, App Store, TikTok…) để một dạng.
- **Giọng văn:** dùng "chúng tôi / we", không dùng "mình / I / one developer".
- **Link ngoài mở tab mới:** mọi link tới store/kênh có `target="_blank" rel="noopener"` (các dòng đang ẩn đã có sẵn, chỉ cần thêm `href`). Link `mailto:` thì không.
- **Không đoán link.** Store, kênh mạng xã hội, trang playtest: hỏi chủ dự án hoặc để ẩn.
- **Không hứa ngày ra mắt** cho game hoặc bản iOS. Chỉ ghi "Coming soon".
- **Phần đầu trang gọn:** người xem phải thấy game mà không cần cuộn. Đừng thêm khối lớn phía trên "Our games".
- **Không viền đen** quanh icon game (chủ dự án không thích). Màu, font và bảng màu theo brand guide: vàng `#FFDE59`, lime `#7ED957`, coral `#FF7A61`, sky `#4DA5FF`, tím `#B66BFF`, mực `#142644`.
- **Không thêm lại** link Privacy trong thẻ game, và link Connect Lights privacy / Delete my data / app-ads.txt trong footer (chủ dự án đã bỏ). Trang xoá dữ liệu vẫn tồn tại ở `connect-lights-privacy-policy/delete-data.html`.
- Sau khi sửa: mở trang ở khoảng 1440px và 390px, kiểm tra hai ngôn ngữ, bấm thử từng link. Chỉ commit/push khi chủ dự án yêu cầu.
