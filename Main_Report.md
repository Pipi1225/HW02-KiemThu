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
Biến định lượng duy nhất được đề cập trong yêu cầu là **độ dài của số điện thoại** (từ 10 đến 11 chữ số).

| Biến định lượng | Min - 1 | Min | Max | Max + 1 |
| :--- | :--- | :--- | :--- | :--- |
| **Độ dài SĐT** | 9 chữ số (Invalid) | 10 chữ số (Valid) | 11 chữ số (Valid) | 12 chữ số (Invalid) |

### 3. Kịch bản kiểm thử (Test Cases)
| Test Case ID | Title | Pre-conditions | Steps | Expected Results | Actual Result / Note | Verdict
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_FR04_01** | Cập nhật thành công với số điện thoại 10 số (Biên Min) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Thay đổi Họ Tên hợp lệ (Ví dụ: `ABC`).<br>2. Nhập Số điện thoại gồm 10 chữ số và bắt đầu bằng số 0 (Ví dụ: `0123456789`).<br>3. Thay đổi Địa chỉ giao hàng mặc định (Ví dụ: `Nguyen Van Cu 101`).<br>4. Nhấn nút "Cập nhật". | Hệ thống lưu thông tin thành công và hiển thị thông báo cập nhật hồ sơ thành công. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_02** | Cập nhật thành công với số điện thoại 11 số (Biên Max) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại gồm 11 chữ số và bắt đầu bằng số 0 (Ví dụ: `01234567890`).<br>2. Nhấn nút "Cập nhật". | Hệ thống lưu thông tin thành công và hiển thị thông báo cập nhật hồ sơ thành công. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_03** | Báo lỗi khi số điện thoại có độ dài thấp hơn giới hạn (Biên Min-1) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại gồm 9 chữ số và bắt đầu bằng số 0 (Ví dụ: `012345678`).<br>2. Nhấn nút "Cập nhật". | Hệ thống hiển thị thông báo lỗi SĐT không hợp lệ (độ dài yêu cầu từ 10-11 chữ số) và không cho phép lưu thay đổi. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_04** | Báo lỗi khi số điện thoại có độ dài vượt quá giới hạn (Biên Max+1) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại gồm 12 chữ số và bắt đầu bằng số 0 (Ví dụ: `012345678901`).<br>2. Nhấn nút "Cập nhật". | Hệ thống hiển thị thông báo lỗi SĐT không hợp lệ hoặc tự động chặn không cho phép nhập ký tự thứ 12. Dữ liệu không được lưu. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_05** | Báo lỗi khi số điện thoại không bắt đầu bằng số 0 | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại hợp lệ về độ dài (10 hoặc 11 số) nhưng bắt đầu bằng ký tự khác số 0 (Ví dụ: `8412345678`).<br>2. Nhấn nút "Cập nhật". | Hệ thống hiển thị thông báo lỗi yêu cầu số điện thoại phải bắt đầu bằng số 0 và không tiến hành lưu dữ liệu. | Hệ thống thông báo "Cập nhật thành công!" và dữ liệu lưu vào hệ thống | Fail |
| **TC_FR04_06** | Kiểm tra lỗi SĐT chứa ký tự chữ cái hoặc ký tự đặc biệt | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại có chứa chữ cái/ký tự đặc biệt (VD: `0123abc789` hoặc `0123-456-789`).<br>3. Nhấn nút "Cập nhật". | Giao diện chặn không cho nhập ký tự lạ hoặc hệ thống báo lỗi: "Số điện thoại chỉ được chứa các chữ số" hoặc "Số điện thoại chứa ký tự không hợp lệ". Không lưu dữ liệu. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_07** | Báo lỗi khi bỏ trống trường Số điện thoại | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Xóa trắng toàn bộ dữ liệu hiện có trong trường "Số điện thoại".<br>2. Đảm bảo các trường thông tin khác (Họ Tên, Địa chỉ) đều hợp lệ.<br>3. Nhấn nút "Cập nhật". | Giao diện hiển thị thông báo lỗi rõ ràng (Ví dụ: "Số điện thoại không được để trống") và không tiến hành lưu dữ liệu. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_08** | Xác nhận trường Email ở trạng thái không thể chỉnh sửa | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Di chuyển chuột hoặc nhấn vào ô nhập liệu của trường "Email".<br>2. Thử thực hiện thao tác xóa, nhập đè hoặc thay đổi nội dung ký tự trong ô Email. | Trường dữ liệu Email ở trạng thái Read-only hoặc Disabled. Người dùng không thể thực hiện bất kỳ thao tác chỉnh sửa nào trên giao diện. | Trường dữ liệu Email ở trạng thái Read-only, không thể thực hiện thao tác chỉnh sửa nào | Pass |
| **TC_FR04_09** | Không thể tự ý thay đổi thuộc tính Role | Người dùng đang đăng nhập với tài khoản có vai trò (Role) hiện tại là "user". | 1. Mở DevTools (F12) > tab **Network** trên trình duyệt.<br>2. Thực hiện cập nhật hồ sơ hợp lệ trên UI để bắt request cập nhật.<br>3. Trích xuất **JWT Token** tại mục `Authorization: Bearer <token>` trong Request Headers.<br>4. Mở công cụ **Postman**, tạo một request PUT để cập nhật (`http://localhost:3000/api/users/me`).<br>5. Tại tab **Authorization**, chọn **Bearer Token** và dán JWT Token vừa lấy được vào mục **Token**.<br>6. Tại tab **Body** (chọn raw > JSON), dán Payload và cố tình chèn thêm role (Ví dụ: `"role": "admin"`).<br>7. Nhấn **Send** và gọi lại API GET Profile (`http://localhost:3000/api/users/me`) để kiểm tra vai trò hiện tại. | Hệ thống loại bỏ/bỏ qua tham số `role` không hợp lệ trong request cập nhật hồ sơ. Thông tin cập nhật các trường khác vẫn thành công nhưng vai trò tài khoản vẫn giữ nguyên là "user". | Sau khi thực hiện lệnh PUT (`http://localhost:3000/api/users/me`) cùng với tham số `role`, hệ thống thông báo đã cập nhật thành công, thông tin được cập nhật và vai trò của tài khoản đổi thành "admin" (trước đó là "user") | Fail |
| **TC_FR04_10** | Không thể cập nhật hồ sơ của tài khoản khác | Hệ thống hiện có tài khoản User A và User B. User A đang thực hiện đăng nhập. | 1. Sử dụng công cụ Developer Tools hoặc Proxy (như Burp Suite) để bắt request cập nhật hồ sơ.<br>2. Thay đổi định danh tài khoản (User ID) trong payload của request từ ID của User A sang ID của User B.<br>3. Gửi request lên server. | Hệ thống từ chối xử lý request, trả về mã lỗi bảo mật (Ví dụ: 403 Forbidden hoặc 401 Unauthorized) và hồ sơ của User B không bị thay đổi. | Test case này không thể thực hiện được, vì backend xác thực bằng JWT chứ không dựa vào trường `userId` từ phía client gửi | Skip |

### 4. AI Gap Analysis
AI đã bao phủ đúng các case chính của FR-04 như cập nhật hồ sơ hợp lệ, kiểm tra biên độ dài SĐT, kiểm tra Email read-only và kiểm tra không được đổi role. Tuy nhiên:

1. Thiếu test case cho SĐT chứa chữ cái/ký tự đặc biệt. Đây là lớp tương đương không hợp lệ riêng theo quy tắc "chỉ chứa chữ số", nên không thể thay thế bằng test case kiểm tra độ dài.
2. Thiếu test case cho SĐT bị để trống. Đây là input invalid phổ biến nhưng AI không suy ra được vì trong đặc tả không nêu rõ ràng SĐT là trường bắt buộc.
3. Có một test case sửa `userId` để cập nhật hồ sơ tài khoản khác không phù hợp với hệ thống thật, vì backend xác thực bằng JWT trong header chứ không dựa vào `userId` do client gửi.

Nguyên nhân chính của các thiếu sót này là xuất phát từ việc AI chỉ phân tích dựa trên bề mặt văn bản, AI thường có xu hướng ưu tiên biên độ dài hơn các lớp tương đương chi tiết, đồng thời thiếu thông tin triển khai backend nên đã sinh ra một test case bảo mật không khả thi. Bản tinh chỉnh FR-04 cuối cùng đã khắc phục bằng cách bổ sung kiểm tra ký tự (`TC_FR04_06`), kiểm tra rỗng (`TC_FR04_07`), và loại bỏ (bỏ qua) kịch bản cập nhật chéo tài khoản (`TC_FR04_10`).

## Feature 2: FR-07: Giỏ hàng (Shopping Cart)
### 1. Phân tích Miền (Domain Analysis)
| Biến đầu vào / Thuộc tính | Lớp tương đương hợp lệ (Valid) | Lớp tương đương không hợp lệ (Invalid) |
| :--- | :--- | :--- |
| **Trạng thái giỏ hàng** | - Giỏ hàng trống (0 sản phẩm)<br>- Giỏ hàng có sản phẩm (>= 1 sản phẩm) | Không có điều kiện loại trừ cụ thể trong context |
| **Thao tác thêm sản phẩm** | - Thêm sản phẩm chưa tồn tại trong giỏ<br>- Thêm sản phẩm đã tồn tại trong giỏ | Không có điều kiện loại trừ cụ thể trong context |
| **Thao tác xóa sản phẩm** | - Xác nhận "Đồng ý" trên Dialog<br>- Xác nhận "Hủy" trên Dialog | Không có điều kiện loại trừ cụ thể trong context |
| **Nhãn hiển thị tổng tiền** | - Hiển thị nhãn "Tổng cộng" | - Hiển thị nhãn "Tổng tạm tính"<br>- Hiển thị bất kỳ nhãn nào khác "Tổng cộng" |

### 2. Phân tích Giá trị biên (Boundary Value Analysis)
Biến định lượng duy nhất được xác định trong context là **số lượng (Quantity)** của một sản phẩm trong giỏ hàng (thao tác thông qua nút +/-). Do context không quy định giới hạn tối đa (Max), các giá trị biên chỉ được áp dụng cho giới hạn tối thiểu (Min = 1).

| Biến định lượng | Min - 1 | Min | Max | Max + 1 |
| :--- | :--- | :--- | :--- | :--- |
| **Số lượng của một sản phẩm** | 0 | 1 | N/A | N/A |

### 3. Kịch bản kiểm thử (Test Cases)
| Test Case ID | Title | Pre-conditions | Steps | Expected Results | Actual Result / Note | Verdict |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_FR07_01** | Kiểm tra hiển thị khi giỏ hàng trống | Người dùng truy cập vào giỏ hàng và chưa chọn mua bất kỳ sản phẩm nào. | 1. Đi đến trang Giỏ hàng. | - Hiển thị hình minh họa giỏ hàng trống.<br>- Hiển thị thông báo rõ ràng về trạng thái giỏ hàng trống. |  |  |
| **TC_FR07_02** | Kiểm tra hiển thị danh sách các cột khi có sản phẩm | Giỏ hàng đã có ít nhất một sản phẩm. | 1. Đi đến trang Giỏ hàng.<br>2. Kiểm tra các cột trong bảng danh sách sản phẩm. | - Hiển thị danh sách sản phẩm với đầy đủ các cột: Sản phẩm, Đơn giá, Số lượng, Thành tiền, Thao tác.<br>- Cột Số lượng phải có nút `+` và `-` để chỉnh sửa. |  |  |
| **TC_FR07_03** | Kiểm tra nhãn hiển thị của Tổng tiền | Giỏ hàng đang có sản phẩm. | 1. Đi đến trang Giỏ hàng.<br>2. Quan sát phần hiển thị tổng số tiền phải thanh toán. | - Nhãn hiển thị chính xác từ: "Tổng cộng".<br>- KHÔNG hiển thị từ "Tổng tạm tính". |  |  |
| **TC_FR07_04** | Kiểm tra thêm cùng một sản phẩm đã có trong giỏ hàng | Giỏ hàng đang có sản phẩm A với Số lượng là 1. | 1. Quay lại trang danh sách sản phẩm.<br>2. Thực hiện thêm sản phẩm A vào giỏ một lần nữa.<br>3. Đi đến trang Giỏ hàng kiểm tra. | - Hệ thống không tạo thêm dòng mới cho sản phẩm A.<br>- Số lượng của sản phẩm A tăng lên thành 2.<br>- Giá trị Thành tiền và Tổng cộng được cập nhật tăng tương ứng. |  |  |
| **TC_FR07_05** | Kiểm tra tăng số lượng sản phẩm bằng nút [+] | Giỏ hàng đang có sản phẩm A với Số lượng là 1. | 1. Đi đến trang Giỏ hàng.<br>2. Nhấn vào nút `+` tại cột Số lượng của sản phẩm A. | - Số lượng sản phẩm A tăng lên thành 2.<br>- Giá trị Thành tiền và Tổng cộng tự động cập nhật chính xác. |  |  |
| **TC_FR07_06** | Kiểm tra giảm số lượng sản phẩm bằng nút [-] (Giá trị Min) | Giỏ hàng đang có sản phẩm A với Số lượng là 2. | 1. Đi đến trang Giỏ hàng.<br>2. Nhấn vào nút `-` tại cột Số lượng của sản phẩm A để giảm về 1. | - Số lượng sản phẩm A giảm xuống còn 1 (Giá trị Min).<br>- Giá trị Thành tiền và Tổng cộng tự động cập nhật chính xác. |  |  |
| **TC_FR07_07** | Kiểm tra nhấn nút [-] khi số lượng đang ở mức tối thiểu (Giá trị Biên Min - 1) | Giỏ hàng đang có sản phẩm A với Số lượng là 1. | 1. Đi đến trang Giỏ hàng.<br>2. Nhấn vào nút `-` tại cột Số lượng của sản phẩm A. | - Hệ thống không cho phép giảm số lượng xuống 0 (Hoặc hiển thị dialog xác nhận xóa sản phẩm tùy theo hành vi xử lý biên của hệ thống). |  |  |
| **TC_FR07_08** | Kiểm tra hủy thao tác xóa sản phẩm qua Dialog xác nhận | Giỏ hàng đang có sản phẩm A. | 1. Đi đến trang Giỏ hàng.<br>2. Nhấn vào nút Xóa tại cột Thao tác của sản phẩm A.<br>3. Trên Dialog xác nhận xuất hiện, nhấn nút "Hủy". | - Xuất hiện Dialog xác nhận trước khi thực hiện xóa.<br>- Khi nhấn "Hủy", Dialog đóng lại.<br>- Sản phẩm A không bị xóa và vẫn giữ nguyên trong giỏ hàng. |  |  |
| **TC_FR07_09** | Kiểm tra đồng ý xóa sản phẩm qua Dialog xác nhận | Giỏ hàng đang có sản phẩm A. | 1. Đi đến trang Giỏ hàng.<br>2. Nhấn vào nút Xóa tại cột Thao tác của sản phẩm A.<br>3. Trên Dialog xác nhận xuất hiện, nhấn nút "Đồng ý/Xác nhận". | - Xuất hiện Dialog xác nhận trước khi thực hiện xóa.<br>- Khi nhấn "Đồng ý/Xác nhận", Dialog đóng lại.<br>- Sản phẩm A bị xóa hoàn toàn khỏi danh sách giỏ hàng.<br>- Giá trị Tổng cộng được tính toán lại chính xác. |  |  |
| **TC_FR07_10** | Kiểm tra chức năng của nút "Tiếp tục mua sắm" | Người dùng đang ở trang Giỏ hàng và giỏ hàng đang trống. | 1. Nhấn vào nút "Tiếp tục mua sắm". | - Hệ thống điều hướng người dùng quay trở về Trang chủ một cách chính xác. |  |  |
| **TC_FR07_11** | Kiểm tra chức năng của nút "Mua tiếp" | Người dùng đang ở trang Giỏ hàng và giỏ hàng đang có một sản phẩm. | 1. Nhấn vào nút "← Mua tiếp". | - Hệ thống điều hướng người dùng quay trở về Trang chủ một cách chính xác. |  |  |
| **TC_FR08_12** | Kiểm tra tính nhất quán trạng thái của giỏ hàng | Người dùng đang ở trang Giỏ hàng và giỏ hàng đang có một sản phẩm. | 1. Nhấn nút refresh trên thanh công cụ (hoặc F5) | Giỏ hàng phải giữ nguyên trạng thái và số lượng các sản phẩm như trước khi Refresh trang |  |  |

### 4. AI Gap Analysis


## Feature 3: FR-15: Product management (CRUD)
### 1. Phân tích Miền (Domain Analysis)

### 2. Phân tích Giá trị biên (Boundary Value Analysis)

### 3. Kịch bản kiểm thử (Test Cases)

### 4. AI Gap Analysis


## Feature 4: FR-20: Hồ sơ cá nhân (FR-04 - Mobile)
### 1. Phân tích Miền (Domain Analysis)

### 2. Phân tích Giá trị biên (Boundary Value Analysis)

### 3. Kịch bản kiểm thử (Test Cases)

### 4. AI Gap Analysis