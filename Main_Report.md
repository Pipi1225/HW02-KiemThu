# HW02: Domain Testing & BVA Report

## Feature 1: FR-04: Quản lý hồ sơ cá nhân
### 1. Phân tích Miền (Domain Analysis)
| Biến đầu vào / Thuộc tính | Lớp tương đương hợp lệ (Valid) | Lớp tương đương không hợp lệ (Invalid) |
| :--- | :--- | :--- |
| **Quyền sở hữu hồ sơ** | Hồ sơ thuộc sở hữu của chính tài khoản đang đăng nhập | Hồ sơ thuộc sở hữu của tài khoản khác |
| **Họ Tên** | Chuỗi ký tự bất kỳ nhập vào | Không có điều kiện loại trừ cụ thể trong context |
| **Số điện thoại (Đầu số)** | Bắt đầu bằng số `0` | Không bắt đầu bằng số `0` |
| **Số điện thoại (Ký tự)** | Chỉ chứa các chữ số | Chứa ký tự chữ cái, khoảng trắng hoặc ký tự đặc biệt |
| **Số điện thoại (Độ dài)** | Độ dài từ 10 đến 11 chữ số | Độ dài < 10 chữ số HOẶC > 11 chữ số |
| **Địa chỉ giao hàng mặc định**| Chuỗi ký tự bất kỳ nhập vào | Không có điều kiện loại trừ cụ thể trong context |
| **Email** | Trạng thái không thể chỉnh sửa (Read-only/Disabled) | Có thể nhập và chỉnh sửa dữ liệu trên giao diện |
| **Role (Quyền hạn)** | Trạng thái giữ nguyên, không thể thay đổi | Có thể thay đổi giá trị thuộc tính role qua giao diện/request |

### 2. Phân tích Giá trị biên (Boundary Value Analysis)
Biến định lượng duy nhất được đề cập trong yêu cầu là độ dài của số điện thoại (từ 10 đến 11 chữ số).

| Biến định lượng | Min - 1 | Min | Max | Max + 1 |
| :--- | :--- | :--- | :--- | :--- |
| **Độ dài SĐT** | 9 chữ số (Invalid) | 10 chữ số (Valid) | 11 chữ số (Valid) | 12 chữ số (Invalid) |

### 3. Kịch bản kiểm thử (Test Cases)
| Test Case ID | Title | Pre-conditions | Steps | Expected Results | Actual Result | Verdict
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_FR04_01** | Cập nhật thành công với số điện thoại 10 số (Biên Min) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Thay đổi Họ Tên hợp lệ (Ví dụ: `ABC`).<br>2. Nhập Số điện thoại gồm 10 chữ số và bắt đầu bằng số 0 (Ví dụ: `0123456789`).<br>3. Thay đổi Địa chỉ giao hàng mặc định (Ví dụ: `Nguyen Van Cu 101`).<br>4. Nhấn nút "Cập nhật". | Hệ thống lưu thông tin thành công và hiển thị thông báo cập nhật hồ sơ thành công. |  |  |
| **TC_FR04_02** | Cập nhật thành công với số điện thoại 11 số (Biên Max) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại gồm 11 chữ số và bắt đầu bằng số 0 (Ví dụ: `01234567890`).<br>2. Nhấn nút "Cập nhật". | Hệ thống lưu thông tin thành công và hiển thị thông báo cập nhật hồ sơ thành công. |  |  |
| **TC_FR04_03** | Báo lỗi khi số điện thoại có độ dài thấp hơn giới hạn (Biên Min-1) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại gồm 9 chữ số và bắt đầu bằng số 0 (Ví dụ: `012345678`).<br>2. Nhấn nút "Cập nhật". | Hệ thống hiển thị thông báo lỗi SĐT không hợp lệ (độ dài yêu cầu từ 10-11 chữ số) và không cho phép lưu thay đổi. |  |  |
| **TC_FR04_04** | Báo lỗi khi số điện thoại có độ dài vượt quá giới hạn (Biên Max+1) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại gồm 12 chữ số và bắt đầu bằng số 0 (Ví dụ: `012345678901`).<br>2. Nhấn nút "Cập nhật". | Hệ thống hiển thị thông báo lỗi SĐT không hợp lệ hoặc tự động chặn không cho phép nhập ký tự thứ 12. Dữ liệu không được lưu. |  |  |
| **TC_FR04_05** | Báo lỗi khi số điện thoại không bắt đầu bằng số 0 | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại hợp lệ về độ dài (10 hoặc 11 số) nhưng bắt đầu bằng ký tự khác số 0 (Ví dụ: `8412345678`).<br>2. Nhấn nút "Cập nhật". | Hệ thống hiển thị thông báo lỗi yêu cầu số điện thoại phải bắt đầu bằng số 0 và không tiến hành lưu dữ liệu. |  |  |
| **TC_FR04_06** | Kiểm tra lỗi SĐT chứa ký tự chữ cái hoặc ký tự đặc biệt | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại có chứa chữ cái/ký tự đặc biệt (VD: `0123abc789` hoặc `0123-456-789`).<br>3. Nhấn nút "Cập nhật". | Giao diện chặn không cho nhập ký tự lạ, hoặc hệ thống báo lỗi: "Số điện thoại chỉ được chứa các chữ số". Không lưu dữ liệu. |  |  |
| **TC_FR04_07** | Xác nhận trường Email ở trạng thái không thể chỉnh sửa | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Di chuyển chuột hoặc nhấn vào ô nhập liệu của trường "Email".<br>2. Thử thực hiện thao tác xóa, nhập đè hoặc thay đổi nội dung ký tự trong ô Email. | Trường dữ liệu Email ở trạng thái Read-only hoặc Disabled. Người dùng không thể thực hiện bất kỳ thao tác chỉnh sửa nào trên giao diện. |  |  |
| **TC_FR04_08** | Kiểm tra bảo mật: Không thể cập nhật hồ sơ của tài khoản khác | Hệ thống hiện có tài khoản User A và User B. User A đang thực hiện đăng nhập. | 1. Sử dụng công cụ Developer Tools hoặc Proxy (như Burp Suite) để bắt request cập nhật hồ sơ.<br>2. Thay đổi định danh tài khoản (User ID) trong payload của request từ ID của User A sang ID của User B.<br>3. Gửi request lên server. | Hệ thống từ chối xử lý request, trả về mã lỗi bảo mật (Ví dụ: 403 Forbidden hoặc 401 Unauthorized) và hồ sơ của User B không bị thay đổi. |  |  |
| **TC_FR04_09** | Kiểm tra bảo mật: Không thể tự ý thay đổi thuộc tính Role | Người dùng đang đăng nhập với tài khoản có vai trò (Role) hiện tại là "User". | 1. Thực hiện điền các thông tin cập nhật hồ sơ.<br>2. Sử dụng công cụ can thiệp request để thêm hoặc sửa đổi tham số thuộc tính gán quyền (Ví dụ: truyền thêm cặp key-value `role: "Admin"`) vào payload request gửi đi.<br>3. Gửi request và kiểm tra lại thông tin vai trò. | Hệ thống loại bỏ/bỏ qua tham số `role` không hợp lệ trong request cập nhật hồ sơ. Thông tin cập nhật các trường khác vẫn thành công nhưng vai trò tài khoản vẫn giữ nguyên là "User". |  |  |

## Feature 2: FR-07: Giỏ hàng (Shopping Cart)
### 1. Phân tích Miền (Domain Analysis)

### 2. Phân tích Giá trị biên (Boundary Value Analysis)

### 3. Kịch bản kiểm thử (Test Cases)

## Feature 3: FR-15: Product management (CRUD)
### 1. Phân tích Miền (Domain Analysis)

### 2. Phân tích Giá trị biên (Boundary Value Analysis)

### 3. Kịch bản kiểm thử (Test Cases)

## Feature 4: FR-20: Hồ sơ cá nhân (FR-04 - Mobile)
### 1. Phân tích Miền (Domain Analysis)

### 2. Phân tích Giá trị biên (Boundary Value Analysis)

### 3. Kịch bản kiểm thử (Test Cases)