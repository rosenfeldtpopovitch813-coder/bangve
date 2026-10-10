# Ghi chú phiên bản tinh chỉnh

- Thay bảng màu tối bằng 40 màu: màu cơ bản bão hòa, pastel, màu đậm và grayscale; thanh công cụ có 12 màu nhanh cùng color picker tùy chỉnh.
- Nét áp lực được lọc nhiễu, nội suy theo đường cong và dựng thành dải nét có bề rộng thay đổi mượt, đầu nét bo tròn.
- Canvas dùng mật độ pixel theo `devicePixelRatio` và mức zoom cho trang đang thao tác; giới hạn mật độ tối đa 4x để tránh tăng bộ nhớ quá mức khi tài liệu có nhiều trang.
- `Ctrl + lăn chuột` zoom giấy; lăn chuột thông thường không bị chặn nên tiếp tục cuộn trang.
- Nét bút vượt đáy A4 được tách sang trang kế; hình học được tiếp nối qua ranh giới trang; chèn văn bản sát đáy sẽ chuyển sang trang kế.
- Chế độ toàn trang giấy dùng trạng thái ẩn/hiện danh sách trang vốn có và lưu lựa chọn trên thiết bị; kích thước logic vẫn là A4 794 × 1123.
- Autosave đặt ở khoảng 220 ms, lưu khi tab bị ẩn, `pagehide` và khi Studio unmount. Bản emergency snapshot theo từng project được ghi vào localStorage khi dữ liệu nhỏ hơn khoảng 2.5 MB và được ưu tiên khi mới hơn bản lưu chính.
- Đã chuẩn hóa đường dẫn ZIP về dấu `/`; `dist/` được tạo lại bằng `npm run build` để tránh gói nhầm bundle cũ.

## Bản sửa tương tác v3 (pointer + zoom anchor)

- Loại bỏ việc tự chuyển sang pan chỉ vì phát hiện pointer thứ hai; mỗi thao tác hiện được khóa theo đúng pointer bắt đầu nét.
- Bỏ trạng thái pointer dễ bị sót khi mất capture, và xóa trạng thái giữ Space khi cửa sổ mất focus để tránh kẹt chế độ di chuyển.
- `Ctrl + lăn chuột` truyền tọa độ con trỏ vào xử lý zoom; giữ điểm trên giấy đang nằm dưới con trỏ làm điểm neo, có bù sai lệch khi vùng cuộn chạm giới hạn.
- Kiểm tra cú pháp TypeScript/TSX cho 18 tệp. Chưa xác nhận `npm run build` vì npm cache không có đầy đủ dependency và registry không truy cập được trong môi trường này.

## Bản v7 (autosave + nút Lưu)

- Thêm nút **Lưu** ở thanh trên cùng (và Ctrl + S dùng chung hàm): chờ kho xác nhận rồi mới báo "Đã lưu lúc hh:mm:ss"; lỗi thì nút đỏ + thông báo. Chấm cam trên nút = còn thay đổi chưa lưu.
- `projectStore.save` đọc lại danh sách sau khi ghi để xác nhận `updatedAt` khớp, không còn báo "đã lưu" khi chưa chắc.
- Trạng thái lưu không còn báo sai: bỏ qua kết quả của lần lưu cũ và không đánh dấu "đã lưu" nếu bài vừa bị sửa tiếp trong lúc đang lưu.
- Mở bài xong chưa chạm gì thì không tự ghi đè/đổi thứ tự thư viện.
- Sửa lỗi lệch dữ liệu khi IndexedDB lỗi: bản ghi tạm vào localStorage nay được ưu tiên đọc lại; đọc IndexedDB trống thì thử localStorage.
- Cảnh báo khi đóng tab lúc còn thay đổi chưa lưu; xin trình duyệt `storage.persist()` để dữ liệu không bị dọn tự động.
- "Nhân đôi" lấy cả bản emergency mới nhất.
