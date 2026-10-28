# IA#2 — Brief: Các prompt thực tế đã gửi cho AI

## Prompt 001 — Part A — Semantic HTML

Ngày: 2026-10-28

Phạm vi: Part A

Công cụ: Codex (GPT-5)

Prompt:

Hãy thực hiện **Part A — Semantic HTML** cho IA#2.

Trước khi sửa, đọc `README.md`, tài liệu đề bài, `index.html`, `app.js`, `style.css` và `check.js`. Xác định chính xác các yêu cầu Part A và cách chạy self-check theo tài liệu của dự án.

1. Sử dụng semantic HTML phù hợp cho các landmark như `header`, `nav`, `main` và `footer`.
2. Đảm bảo trang có đúng một `h1`, thứ bậc heading hợp lý và tên sản phẩm dùng heading phù hợp.
3. `#catalogue` phải là danh sách sản phẩm đúng cấu trúc; mỗi card sản phẩm dùng phần tử list phù hợp, kể cả trong template.
4. Input tìm kiếm `#q` phải có label liên kết đúng và nằm trong một `form`.
5. Các nút tương tác phải là phần tử `button` thực sự, không dùng `div` giả làm nút.
6. Nút Add của sản phẩm Sold out phải có thuộc tính `disabled`.
7. Giữ nguyên ID, class, selector, dữ liệu sản phẩm và các cấu trúc cần thiết để CSS và JavaScript hoạt động.

- Chỉ sửa `index.html` cho Part A, trừ khi phát hiện lý do kỹ thuật bắt buộc cần sửa file khác; nếu có, hãy báo trước.
- Không sửa `style.css` hoặc `check.js`.
- Chưa triển khai logic B1, B2, B3 hoặc B4.
- Không commit hoặc push.

Chạy self-check theo README hoặc cách chạy được dự án hỗ trợ. Mục tiêu là `8/8 passed`. Nếu chưa đạt, xác định lỗi, sửa trong phạm vi Part A và kiểm tra lại. Không được tuyên bố thành công nếu chưa có kết quả thực tế.

Sau đó báo:

- Những thay đổi đã thực hiện.
- Kết quả của từng self-check.
- File đã thay đổi.
- Diff có nằm đúng phạm vi Part A không.
- Lệnh Git đề xuất để tôi kiểm tra và commit.

Dừng lại và chờ tôi xác nhận trước khi làm B1.
