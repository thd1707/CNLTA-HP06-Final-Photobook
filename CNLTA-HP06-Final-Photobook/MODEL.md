# 📦 Data Model – MyPhotoBook SwiftUI App

Một cấu trúc dữ liệu đầy đủ cho app **sách ảnh cá nhân**, hỗ trợ chọn template, tạo nhiều trang ảnh với chú thích, và lưu layout tùy theo từng template.

---

## 🧱 1. Các Model chính

### ✅ `PhotoBook` – đại diện cho **một cuốn sách ảnh**

```swift
struct PhotoBook: Identifiable, Codable {
    var id: UUID = UUID()
    var title: String
    var template: Template
    var pages: [PhotoPage]
}
📌 Gồm:

title: Tên do người dùng nhập.

template: Thông tin giao diện bìa & layout.

pages: Danh sách trang ảnh.

✅ PhotoPage – đại diện cho một trang trong sách
swift
Copy
Edit
struct PhotoPage: Identifiable, Codable {
    var id: UUID = UUID()
    var imageDataList: [Data]   // Mảng ảnh (cho phép 1–n ảnh tuỳ layout)
    var captions: [String]      // Mảng chú thích (mỗi ảnh 1 caption)
    var date: Date              // Ngày tạo
}
📌 Ghi chú:

Hỗ trợ layout có nhiều ảnh (VD: 2 ảnh/trang).

Ảnh và caption được lưu đồng bộ.

✅ Template – đại diện cho mẫu bìa và bố cục
swift
Copy
Edit
struct Template: Identifiable, Codable {
    var id: UUID = UUID()
    var name: String
    var backgroundColorHex: String   // VD: "#FFDDEE"
    var fontName: String
    var coverImageName: String
    var layout: TemplateLayout
    var previewImageName: String     // Ảnh mô tả layout khung xám
}
📌 Gồm:

layout: Kiểu trình bày cố định cho tất cả trang trong sách.

previewImageName: Dùng để hiện layout mẫu trực quan trong danh sách chọn template.

✅ TemplateLayout – đại diện cho kiểu bố cục trang
swift
Copy
Edit
enum TemplateLayout: String, Codable {
    case fullImage           // 1 ảnh to toàn trang
    case imageWithCaption    // 1 ảnh + caption bên dưới
    case twoImages           // 2 ảnh chia đôi trang
}
📂 2. Lưu trữ dữ liệu
Trong PhotoBookViewModel.swift:

swift
Copy
Edit
@Published var photoBooks: [PhotoBook] = [] {
    didSet {
        saveBooks()
    }
}

func saveBooks() {
    if let encoded = try? JSONEncoder().encode(photoBooks) {
        UserDefaults.standard.set(encoded, forKey: "SavedPhotoBooks")
    }
}

func loadBooks() {
    if let data = UserDefaults.standard.data(forKey: "SavedPhotoBooks"),
       let decoded = try? JSONDecoder().decode([PhotoBook].self, from: data) {
        self.photoBooks = decoded
    }
}
📌 Tips:

Nếu ảnh nặng, dùng FileManager để lưu ảnh ngoài rồi chỉ lưu đường dẫn.

📚 Tổng kết luồng dữ liệu
Thành phần    Vai trò    Quan hệ
PhotoBook    Cuốn sách    Gồm nhiều PhotoPage, gắn với Template
PhotoPage    Một trang    Chứa 1 hoặc nhiều ảnh + caption
Template    Giao diện mẫu    Gồm style bìa + bố cục TemplateLayout
TemplateLayout    Loại bố cục    Áp dụng cố định cho mọi trang trong sách
PhotoBookViewModel    Quản lý dữ liệu    Chứa danh sách photobook
UserDefaults    Lưu dữ liệu đơn giản    Lưu toàn bộ JSON
previewImageName    Hình preview layout    Giúp người dùng chọn template dễ hình dung

💡 Gợi ý mở rộng
Cho phép người dùng chọn layout từng trang (hiện đang áp dụng 1 layout cho cả sách).

Thêm hỗ trợ đổi màu nền từng trang.

Giao diện preview layout tương tác — xem thử từng trang mẫu trước khi chọn.

Thêm watermark logo hoặc ký tên cuối sách.





