# AI-LOG.md

## Bảng tổng hợp quá trình sử dụng AI

| STT | Ngày       | Phần              | Công cụ                                    | Yêu cầu / Công việc                                                                         | Nội dung thay đổi                                                                                                                                        | Phương án từ chối / Không sử dụng                                                          | Kiểm chứng                                                                                                                                       | Commit      |
| --: | ---------- | ----------------- | ------------------------------------------ | ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ | ----------- |
| 001 | 2026-10-28 | Part A / kiểm thử | Codex (GPT-5), PowerShell, Chrome headless | Thực hiện Part A — Semantic HTML; đạt self-check 8/8; cập nhật brief và AI-LOG; chưa làm B1 | Sửa semantic structure trong `index.html`: landmark, heading, form, list/card, label, button và disabled Add. Tạo `brief.md` và `AI-LOG.md` theo yêu cầu | Không sửa `app.js`, `style.css` hoặc `check.js`; không triển khai B1–B4; không commit/push | Chrome headless tải `index.html`; Console của `check.js` ghi `Session 4 self-check: 8/8 passed`; 8/8 dòng PASS. `git diff --check` không báo lỗi | Chưa commit |

## Nhật ký chi tiết

### Lần tương tác 001 — Part A — Semantic HTML

Ngày: 2026-10-28

Phần: Part A

Công cụ: Codex (GPT-5)

Yêu cầu: Thực hiện Part A — Semantic HTML theo prompt thực tế được lưu đầy đủ trong `brief.md`; chỉ sửa `index.html` cho Part A, cập nhật hai tài liệu, chạy self-check đạt 8/8 và dừng trước B1.

File đã thay đổi: `index.html`, `brief.md`, `AI-LOG.md`

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
