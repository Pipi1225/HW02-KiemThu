## Pool A — Authentication, Categories, and Products
### FR-04: Quản lý hồ sơ cá nhân
- Người dùng đã đăng nhập có thể cập nhật: Họ Tên, Số điện thoại, Địa chỉ giao hàng mặc định.
- Số điện thoại hợp lệ: bắt đầu bằng số 0, từ 10–11 chữ số.
- Email không được phép thay đổi qua giao diện.
- Người dùng chỉ có thể cập nhật hồ sơ của chính mình; không thể tự thay đổi thuộc tính role.

## Pool B — Shopping Cart and Checkout
### FR-07: Giỏ hàng (Shopping Cart)
- Hiển thị danh sách sản phẩm với các cột: Sản phẩm, Đơn giá, Số lượng (có nút +/- để chỉnh), Thành tiền, Thao tác.
- Thêm cùng một sản phẩm vào giỏ sẽ tăng số lượng, không tạo dòng mới.
- Nút Xóa sản phẩm phải có dialog xác nhận trước khi thực hiện.
- Có nút Tiếp tục mua sắm để quay về trang chủ.
- Tổng tiền hiển thị nhãn chính xác: "Tổng cộng" (không phải "Tổng tạm tính").
- Giỏ hàng trống phải có hình minh họa và thông báo rõ ràng.

## Pool C — Web Admin
### FR-15: Product management (CRUD)
- Admin có thể Thêm / Xem / Sửa / Xóa sản phẩm.
- Ràng buộc đầu vào:
    - Tên sản phẩm: bắt buộc, tối đa 255 ký tự.
    - Giá: bắt buộc, phải là số dương (> 0).
    - Danh mục: bắt buộc, phải chọn từ danh sách có sẵn.
- Khi Sửa một sản phẩm, chỉ sản phẩm đó bị thay đổi — các sản phẩm khác giữ nguyên.

## Pool D — Mobile App - Expo
### FR-20: Hồ sơ cá nhân (giống FR-04)