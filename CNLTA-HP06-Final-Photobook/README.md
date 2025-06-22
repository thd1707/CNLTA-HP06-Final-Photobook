# 📘 PhotoBook SwiftUI App

Ứng dụng SwiftUI cho phép người dùng tạo photobook điện tử cá nhân hóa sau các chuyến đi chơi, kỷ niệm,... Người dùng có thể chọn template với layout cố định, đặt tên cuốn sách ảnh, thêm từng trang gồm ảnh + chú thích, và xem lại album với giao diện đẹp mắt.

---

## 🎯 Mục tiêu sản phẩm

- Cho phép người dùng:
  - Chọn **template layout** từ danh sách có sẵn.
  - Đặt tên cuốn **photobook**.
  - Thêm từng **trang ảnh** (1 hoặc nhiều ảnh tùy layout).
  - Nhập **chú thích ngắn** cho ảnh.
  - **Xem lại photobook** với giao diện tương ứng layout template đã chọn.

---

## 🛠️ Các chức năng chính

### 1. 📖 Chọn template & đặt tên photobook
- Template có sẵn gồm: Classic, Collage, Polaroid...
- Mỗi template quy định **layout cố định** cho toàn bộ các trang (VD: Classic = 1 ảnh/trang, Collage = 2 ảnh/trang).
- Template được hiển thị bằng **preview trực quan** (khung xám mô tả layout từng trang).
- Người dùng đặt tên cho cuốn sách (VD: “Trip to Đà Lạt”, “Summer Memories 2025”).

### 2. 🖼️ Thêm trang ảnh
- Chọn ảnh từ **thư viện máy (PHPicker)**.
- Nhập chú thích cho từng ảnh.
- App kiểm tra **số ảnh đúng với layout template đã chọn** (VD: template Collage yêu cầu đúng 2 ảnh/trang).
- Không cho thêm trang nếu chưa đủ ảnh phù hợp với layout.

### 3. 📚 Xem lại photobook
- Dùng `ScrollView` hoặc `TabView` để hiển thị lần lượt từng trang.
- Layout mỗi trang được hiển thị đúng theo **template đã chọn**.
- Có thể chỉnh sửa, xoá trang, hoặc thêm mới.

---

## 📂 Cấu trúc dữ liệu

- `Template`: quy định layout và style (VD: Classic, Polaroid).
- `PhotoBook`: gồm title + template + danh sách trang (`PhotoPage`).
- `PhotoPage`: chứa ảnh và chú thích, định dạng theo layout template.

---

## 📚 Kiến thức SwiftUI áp dụng

- `@State`, `@Binding`, `@StateObject`, `@ObservedObject`
- `TabView`, `ScrollView`, `NavigationView`
- `PHPickerViewController` qua `UIViewControllerRepresentable`
- Tuỳ biến layout qua enum `TemplateLayout`
- Hiển thị preview layout template
- Kiểm tra logic dữ liệu phù hợp layout trước khi thêm

---

## 🚀 Phát triển tương lai

- Tạo nhiều photobook, chuyển đổi giữa các album.
- Hỗ trợ chia sẻ hoặc xuất PDF.
- Dark Mode, font chữ đẹp, sticker,...
- Drag & drop để sắp xếp lại trang.
- Template có layout động (cho phép chọn layout từng trang sau này).
