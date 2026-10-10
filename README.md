# Lớp học Mực

Bảng viết tay chạy trên trình duyệt, xây dựng lại theo hướng sử dụng của Scrble Ink từ gói `.appx` người dùng cung cấp. Giao diện mở vào giấy A4 dọc kẻ dòng, có lề đỏ và cột hình thu nhỏ trang bên trái; thanh công cụ đặt ngang để tập trung vào viết, vẽ, tẩy, lật trang. Đây là sản phẩm độc lập lấy cảm hứng từ Scrble Ink, không chứa mã nguồn của ứng dụng đó.

## Chạy trên máy

```bash
npm install
npm run build
npm run preview
```

Mở địa chỉ Vite hiển thị trong cửa sổ lệnh. Thư mục `dist/` là bản web tĩnh có thể triển khai.

## Đã có

- 13 kiểu bút gồm bút bi, bút chì, bút máy, bút cọ, bút lông, dạ quang, phấn, sáp màu và neon; nét liền, nét đứt, nét chấm; màu, độ dày, độ mờ và lực nhấn.
- Tẩy cả nét, tẩy một phần nét, xóa đối tượng; chọn, di chuyển, đổi kích thước, xoay, nhân đôi, sao chép và dán.
- Hình học, chữ tiếng Việt, công thức Hóa học với chỉ số Unicode và xem trước LaTeX bằng KaTeX.
- Giấy trống, kẻ dòng, ô vuông, chấm, đồ thị và một số mẫu giấy; đổi màu giấy, đường kẻ, khoảng cách, ảnh nền.
- 19 hình vẽ, bút laser với chấm/vòng tròn/vùng sáng và pop-up tùy chọn riêng cho từng công cụ.
- Nhiều trang A4 liền mạch khi cuộn, chỉ ngăn nhau bởi một đường 1 px; tự tạo/chuyển trang khi nét viết vượt đáy A4; hình học được tiếp nối qua mép trang và văn bản gần đáy được đưa sang trang tiếp theo. Có hình thu nhỏ, đổi tên, nhân đôi, xóa, kéo đổi thứ tự; Ctrl + kéo hoặc Ctrl + lăn chuột để zoom, lăn chuột thường vẫn cuộn giấy; hoàn tác và làm lại.
- Nhập PDF thành các trang để viết trực tiếp, chèn ảnh; xuất PNG, JPG, PDF, SVG; tự lưu trên thiết bị bằng IndexedDB với nhịp autosave khoảng 220 ms, flush khi tab bị ẩn/rời trang và emergency snapshot localStorage giới hạn khoảng 2.5 MB để phục hồi bản mới hơn nếu ghi IndexedDB bị gián đoạn.
- Trang chủ dạng thư viện để tạo, tìm, đổi tên, nhân đôi và xóa project. Mỗi project lưu tài liệu và các trang riêng; bài viết cũ tự được đưa vào thư viện khi mở phiên bản mới.
- Nút chế độ toàn trang giấy ẩn/hiện danh sách trang để mở rộng vùng A4; lựa chọn này được nhớ trên thiết bị. Bảng màu có 40 màu tươi gồm màu cơ bản, pastel, màu đậm và grayscale, cùng thanh màu nhanh và màu tùy chỉnh. Nét pressure được nội suy mượt và canvas tăng mật độ render theo devicePixelRatio/zoom để chữ viết giữ độ sắc nét.

## Giới hạn

Tài liệu và nét viết hiện lưu trên thiết bị đang dùng, chưa đồng bộ nhiều người hoặc cung cấp phòng học âm thanh/video. PDF và ảnh được nhúng vào dữ liệu cục bộ, nên tài liệu rất lớn có thể vượt dung lượng bộ nhớ trình duyệt. Nhập DOCX/PPTX trực tiếp cần dịch vụ chuyển đổi riêng. Công thức LaTeX được xem trước bằng KaTeX; khi chèn lên giấy, biểu thức phổ biến được chuyển thành chữ Unicode để đảm bảo tương thích công cụ viết và xuất.

`ProjectStore`, `DocumentStore` và các kiểu dữ liệu trong `src/types` tách khỏi giao diện để sau này nối với dịch vụ đồng bộ thực tế.
