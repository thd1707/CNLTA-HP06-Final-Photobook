

# 📦 Data Model – MyPhotoBook SwiftUI App


## 🧱 1. Các Model chính

### ✅ `PhotoBook` – đại diện cho **một cuốn sách ảnh**

```swift
struct PhotoBook: Identifiable, Codable {
    var id: UUID = UUID()
    var title: String         // Tên cuốn sách (VD: "Trip to Đà Lạt")
    var template: Template    // Mẫu giao diện đã chọn
    var pages: [PhotoPage]    // Các trang trong cuốn sách
}
```

📌 **Giải thích:**

* `title`: Tên do người dùng nhập khi tạo photobook.
* `template`: Lưu lại mẫu người dùng chọn (xem chi tiết bên dưới).
* `pages`: Danh sách các trang ảnh trong photobook.

---

### ✅ `PhotoPage` – đại diện cho **một trang trong sách**

```swift
struct PhotoPage: Identifiable, Codable {
    var id: UUID = UUID()
    var imageData: Data       // Ảnh dưới dạng binary (nén từ UIImage)
    var caption: String       // Ghi chú của người dùng
    var date: Date            // Ngày tạo trang
}
```

📌 **Giải thích:**

* `imageData`: Dùng để lưu ảnh đã chọn (từ thư viện).
* `caption`: Nội dung chú thích ảnh (VD: "Chợ đêm Đà Lạt").
* `date`: (tuỳ chọn) để sắp xếp theo thời gian.

---

### ✅ `Template` – đại diện cho **giao diện bìa**

```swift
struct Template: Identifiable, Codable {
    var id: UUID = UUID()
    var name: String            // Tên template (VD: "Pastel Pink")
    var backgroundColor: Color  // Màu nền chính (hoặc lưu dạng Hex/String nếu dùng UserDefaults)
    var fontName: String        // Font chữ
    var coverImageName: String  // Tên ảnh dùng làm hình bìa
}
```

📌 **Giải thích:**

* Template giúp cá nhân hoá mỗi cuốn sách ảnh theo màu & phong cách.

---

## 📂 2. Lưu trữ dữ liệu

### ✅ Lưu danh sách PhotoBook:

* Dùng `@Published var photoBooks: [PhotoBook]` trong `PhotoBookViewModel`
* Lưu và tải với `UserDefaults` hoặc `FileManager`

```swift
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
```

---

## 📚 Tổng kết luồng dữ liệu

| Thành phần                 | Vai trò         | Mối quan hệ                                |
| -------------------------- | --------------- | ------------------------------------------ |
| `PhotoBook`                | Cuốn sách chính | Gồm nhiều `PhotoPage`, gắn với `Template`  |
| `PhotoPage`                | Một trang ảnh   | Chứa ảnh + chú thích                       |
| `Template`                 | Giao diện mẫu   | Quyết định kiểu hiển thị bìa               |
| `PhotoBookViewModel`       | Quản lý dữ liệu | Chứa danh sách tất cả photobook            |
| `UserDefaults/FileManager` | Lưu trữ cục bộ  | Lưu lại các photobook sau mỗi lần thêm/sửa |

---

👉 **Gợi ý mở rộng:**

* Cho phép nhiều photobook, mỗi photobook như một "folder".
* Cho phép export thành PDF, chia sẻ.
* Hỗ trợ drag-drop reorder trang trong photobook.



