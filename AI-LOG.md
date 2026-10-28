# AI-LOG.md

## Bảng tổng hợp quá trình sử dụng AI

| STT | Ngày       | Phần              | Công cụ                                                              | Yêu cầu / Công việc                                                                         | Nội dung thay đổi                                                                                                                                                 | Phương án từ chối / Không sử dụng                                                                       | Kiểm chứng                                                                                                                                                                                                        | Commit      |
| --: | ---------- | ----------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| 001 | 2026-10-28 | Part A / kiểm thử | Codex (GPT-5), PowerShell, Chrome headless                           | Thực hiện Part A — Semantic HTML; đạt self-check 8/8; cập nhật brief và AI-LOG; chưa làm B1 | Sửa semantic structure trong `index.html`: landmark, heading, form, list/card, label, button và disabled Add. Tạo `brief.md` và `AI-LOG.md` theo yêu cầu          | Không sửa `app.js`, `style.css` hoặc `check.js`; không triển khai B1–B4; không commit/push              | Chrome headless tải `index.html`; Console của `check.js` ghi `Session 4 self-check: 8/8 passed`; 8/8 dòng PASS. `git diff --check` không báo lỗi                                                                  | Chưa commit |
| 002 | 2026-10-28 | B1 / kiểm thử     | Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol | Chỉ hoàn thành B1 — Add to Cart bằng event delegation trên `#catalogue`                     | Sửa `app.js`: thêm một listener click trên `#catalogue`, kiểm tra `.add`, tìm `.card`, chặn disabled/Sold out, cập nhật `cart` và `cart-count` bằng `textContent` | Không sửa `index.html`, `style.css`, `check.js` hoặc logic B2–B4; không gắn listener riêng cho từng nút | Lần chạy inline đầu thất bại do quoting PowerShell trước khi kiểm thử. Lần chạy lại thành công: T-shirt 2 lần → `2`; Tote Sold out → vẫn `2`; Load more tạo 12 card; Belt → `3`. `git diff --check` không báo lỗi | Chưa commit |
| 003 | 2026-10-28 | B2 / kiểm thử     | Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol | Chỉ hoàn thành B2 — Filter as you type                                                      | Sửa `app.js`: thêm lọc theo input, trim/lowercase, ẩn/hiện card, status bằng `textContent` và listener `input`                                                    | Không sửa `index.html`, `style.css`, `check.js` hoặc B1/B3/B4; không dùng `innerHTML`                   | Chrome DevTools Protocol: `scarf` và `SCARF` đều 1/8; rỗng hiện lại 8 card và status rỗng; sau Load more có 12 card; chuỗi HTML cho 0 kết quả, giữ nguyên status, 0 ảnh, 0 alert                                  | Chưa commit |
| 004 | 2026-10-28 | B3 / kiểm thử     | Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol | Chỉ hoàn thành B3 — Prevent form reload                                                     | Sửa `app.js`: lấy form bằng `searchInput.form`, chặn `submit` bằng `event.preventDefault()`, gọi `applyFilter()`                                                  | Không sửa `index.html`, `style.css`, `check.js` hoặc B1/B2/B4                                           | Chrome DevTools Protocol: thêm T-shirt 2 lần, nhập `cap`, nhấn Enter; URL không có `?q=cap`, cart vẫn `2`, status `Showing 1 of 8 products`                                                                       | Chưa commit |

## Nhật ký chi tiết

### Lần tương tác 001 — Part A — Semantic HTML

Ngày: 2026-10-28

Phần: Part A

Công cụ: Codex (GPT-5)

Yêu cầu: Thực hiện Part A — Semantic HTML theo prompt thực tế được lưu đầy đủ trong `brief.md`; chỉ sửa `index.html` cho Part A, cập nhật hai tài liệu, chạy self-check đạt 8/8 và dừng trước B1.

File đã thay đổi: `index.html`

Nội dung thay đổi:

- Đổi thanh trên cùng thành `header`, menu thành `nav`, nội dung thành `main`, chân trang thành `footer`.
- Đổi tiêu đề Catalogue thành đúng một `h1`; tên sản phẩm thành `h2`.
- Đổi `#catalogue` thành `ul`; tất cả card hiện tại và card trong `#card-template` thành `li`.
- Đổi vùng tìm kiếm thành `form`, thêm `label for="q"` liên kết với input `#q`.
- Đổi Search, Add và Load more thành phần tử `button` thực sự.
- Thêm thuộc tính `disabled` cho nút Add của Tote bag Sold out.
- Giữ nguyên ID, class, selector và dữ liệu sản phẩm; không thay đổi `app.js`.

Phương án từ chối: Không sửa `style.css`, `check.js` hoặc `app.js`; không dùng `div` làm nút; không triển khai logic B1–B4; không commit hoặc push, đúng giới hạn của yêu cầu.

Kiểm chứng: Chạy `git diff --check` — không phát hiện lỗi whitespace. Chạy Chrome headless với file `index.html`; Console ghi `Session 4 self-check: 8/8 passed`. Kết quả từng dòng: 1 PASS landmarks; 2 PASS exactly one h1; 3 PASS heading levels; 4 PASS product names are headings; 5 PASS catalogue list and cards; 6 PASS connected label; 7 PASS search inside form; 8 PASS real buttons and no onclick.

Lỗi phát hiện: Không phát hiện lỗi trong Part A.

### Lần tương tác 002 — B1 — Add to Cart

Ngày: 2026-10-28

Phần: B1 / kiểm thử

Công cụ: Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol

Yêu cầu: Đọc README.md và app.js, chỉ hoàn thành B1 — Add to Cart với một click listener trên `#catalogue`, event delegation, `closest('.card')`, cập nhật `cart-count`, bỏ qua disabled/Sold out, không sửa các file ngoài phạm vi; sau đó kiểm tra T-shirt, Tote bag, Load more và Belt.

File đã thay đổi: `app.js`

Nội dung thay đổi: Thêm duy nhất một `catalogue.addEventListener('click', ...)`; lấy `.add` và `.card` bằng `closest`; bỏ qua nút có class `disabled`, thuộc tính `disabled` hoặc trạng thái `Sold out`; cập nhật `cart[id]` và dùng `cartCount.textContent` trong `renderCart()`. Không triển khai B4 nên `cart-total` vẫn chưa được xử lý.

Phương án từ chối: Không sửa `index.html`, `style.css`, `check.js`; không gắn listener riêng lên từng nút; không triển khai B2, B3 hoặc B4.

Kiểm chứng: Lần thử đầu không chạy được do lỗi quoting của lệnh PowerShell, trước khi bài kiểm thử được thực thi. Lần chạy lại bằng Chrome DevTools Protocol thực thi được các thao tác: click T-shirt hai lần, dispatch click thử lên Tote Sold out, click Load more, click Belt. Kết quả: `before: "2"`, `afterTote: "2"`, `afterBelt: "3"`, `cards: 12`, `belt: true`. Đã chạy `git diff --check`, không phát hiện lỗi whitespace.

Lỗi phát hiện: Lỗi quoting ở lần chạy kiểm thử đầu, đã khắc phục bằng script CDP mã hóa; không phát hiện lỗi B1 trong lần kiểm thử thành công.

### Lần tương tác 003 — B2 — Filter as you type

Ngày: 2026-10-28

Phần: B2 / kiểm thử

Công cụ: Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol

Yêu cầu: Chỉ hoàn thành B2 — Filter as you type; lọc theo `#q` khi có sự kiện `input`, không phân biệt hoa thường, dùng `card.hidden`, hiển thị status đúng định dạng bằng `textContent`, không chạy HTML người dùng và chỉ sửa `app.js`.

File đã thay đổi: `app.js`Tiếp tục từ code hiện tại. Chỉ hoàn thành B2 — Filter as you type.

Yêu cầu:

1. Khi input #q phát sinh sự kiện input, gọi applyFilter().
2. Đọc giá trị tìm kiếm, dùng trim() và toLowerCase() để lọc không phân biệt chữ hoa/chữ thường.
3. Duyệt các phần tử .card và đặt card.hidden dựa trên việc tên sản phẩm có chứa từ khóa hay không.
4. Nếu từ khóa rỗng sau khi trim(), hiển thị lại tất cả sản phẩm và để statusBox trống.
5. Nếu có kết quả, hiển thị đúng định dạng "Showing X of Y products", trong đó Y là tổng số thẻ sản phẩm hiện có.
6. Nếu không có kết quả, hiển thị 'No products match "..."', giữ nguyên chính xác nội dung người dùng nhập trong thông báo.
7. Chỉ dùng textContent để hiển thị nội dung. Tuyệt đối không dùng innerHTML cho dữ liệu người dùng.
8. Chỉ sửa app.js; giữ nguyên tất cả id, class, style.css và check.js.

Sau khi sửa, hướng dẫn tôi kiểm tra các từ khóa scarf, SCARF, chuỗi rỗng và <img src=x onerror=alert(1)>. Giải thích vì sao trường hợp cuối không được chạy mã JavaScript.

Nội dung thay đổi: `applyFilter()` đọc giá trị gốc và giá trị đã `trim().toLowerCase()`, duyệt các card trong `#catalogue`, cập nhật `hidden`, đếm kết quả trên tổng số card hiện có, dùng `statusBox.textContent`, và đăng ký `searchInput.addEventListener('input', applyFilter)`.

Phương án từ chối: Không sửa `index.html`, `style.css`, `check.js`; không dùng `innerHTML`; không thay đổi B1 hoặc triển khai B3/B4.

Kiểm chứng: Chrome DevTools Protocol nhập `scarf` → `Scarf`, status `Showing 1 of 8 products`; nhập `SCARF` → cùng kết quả; xóa ô → 8 card hiện lại, status rỗng; Load more → 12 card; nhập `<img src=x onerror=alert(1)>` → không card, status `No products match "<img src=x onerror=alert(1)>"`, `images: 0`, `alerts: 0`.

Lỗi phát hiện: Không phát hiện lỗi B2 trong kiểm thử thành công. Chuỗi cuối không chạy JavaScript vì được đưa vào `textContent` của status, không được phân tích như HTML.

### Lần tương tác 004 — B3 — Prevent form reload

Ngày: 2026-10-28

Phần: B3 / kiểm thử

Công cụ: Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol

Yêu cầu: Chỉ hoàn thành B3 bằng `searchInput.form`, chặn submit bằng `event.preventDefault()`, gọi `applyFilter()`, giữ trạng thái giỏ hàng và kiểm tra nhập `cap` rồi nhấn Enter.

File đã thay đổi: `app.js`

Nội dung thay đổi: Đăng ký listener `submit` trên `searchInput.form`; gọi `event.preventDefault()` để ngăn hành vi submit mặc định và gọi `applyFilter()` để cập nhật kết quả.

Phương án từ chối: Không sửa `index.html`, `style.css`, `check.js`; không thay đổi B1, B2 hoặc B4.

Kiểm chứng: Chrome DevTools Protocol thêm T-shirt hai lần, nhập `cap`, phát sinh phím Enter. Kết quả: URL không có `?q=cap`; cart là `2`; status là `Showing 1 of 8 products`; form tồn tại.

Lỗi phát hiện: Không phát hiện lỗi B3 trong kiểm thử thành công. Enter mặc định submit form vì input nằm trong form và trình duyệt thực hiện submit khi nhấn Enter; `preventDefault()` hủy hành vi tải lại và thay đổi URL mặc định.
