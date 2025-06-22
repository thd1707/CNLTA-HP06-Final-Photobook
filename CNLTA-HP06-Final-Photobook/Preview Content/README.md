# 📘 PhotoBook SwiftUI App

Một ứng dụng SwiftUI tối giản (MVP) cho phép người dùng tạo sách ảnh cá nhân sau mỗi chuyến đi chơi, sự kiện, hoặc kỷ niệm đáng nhớ. Người dùng có thể chọn template, đặt tên photobook, thêm từng trang với ảnh + chú thích và xem lại album với giao diện đẹp mắt.

---

## 🎯 Mục tiêu sản phẩm

- Tạo một photobook điện tử cá nhân hóa.
- Cho phép người dùng:
  - Chọn **mẫu template** có sẵn.
  - Đặt **tên cuốn sách ảnh**.
  - Thêm từng trang ảnh với **ảnh từ thư viện** và **ghi chú ngắn**.
  - **Xem lại album** với layout dễ nhìn.
- Giao diện đơn giản, đẹp, phù hợp học sinh – sinh viên hoặc người mới học lập trình SwiftUI.

---

## 🛠️ Các chức năng chính

### 1. 📖 Template chọn bìa photobook
- Người dùng chọn một trong nhiều mẫu template có sẵn (màu sắc, font, hình bìa...).
- Có thể đặt tên cho photobook (VD: *Summer 2025*, *Trip to Đà Lạt*...).

### 2. 🖼️ Thêm trang ảnh
- Người dùng chọn ảnh từ **thư viện máy**.
- Thêm **chú thích ngắn** cho từng ảnh (VD: "Hồ Xuân Hương lúc sáng", "ăn bánh căn nè").
- Ảnh và chú thích được lưu lại như một "trang" của cuốn sách.

### 3. 👀 Xem lại photobook
- Dùng `ScrollView` hoặc `TabView` để xem lần lượt từng ảnh như lật trang sách.
- Mỗi ảnh có hiển thị chú thích dưới hình.
- Giao diện tinh gọn, dễ nhìn, tối ưu cho điện thoại.


## 📚 Kiến thức SwiftUI áp dụng
- `@State`, `@ObservedObject`, `@StateObject`, `@Binding`
- `List`, `Form`, `ScrollView`, `NavigationView`, `TabView`
- `PHPickerViewController` tích hợp chọn ảnh từ thư viện (via `UIViewControllerRepresentable`)
- Lưu dữ liệu với `UserDefaults` hoặc `FileManager` (tuỳ phiên bản)
- Tuỳ biến UI theo template đã chọn

---

## 🚀 Phát triển tương lai (vượt MVP)
- Cho phép sắp xếp lại thứ tự trang ảnh
- Tạo nhiều photobook, quản lý mỗi cuốn như 1 "folder"
- Export sang PDF (nâng cao)
- Chế độ Dark Mode
- Thêm ảnh nền hoặc sticker, font chữ đẹp
