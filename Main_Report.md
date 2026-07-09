# HW02: Domain Testing & BVA Report

## Feature 1: FR-04: Quản lý hồ sơ cá nhân
### 1. Phân tích Miền (Domain Analysis)
Dựa trên đặc tả hệ thống, chức năng Quản lý hồ sơ cá nhân bao gồm 8 biến đầu vào chính: Quyền sở hữu hồ sơ, Họ Tên, Số điện thoại (đầu số), Số điện thoại (ký tự), Số điện thoại (độ dài), Địa chỉ giao hàng mặc định, Email và Role.

1. Biến đầu vào: Quyền sở hữu hồ sơ
    - Lớp hợp lệ: 
        - A1 - Chỉnh sửa hồ sơ thuộc sở hữu của chính tài khoản đang đăng nhập.
    - Lớp không hợp lệ: 
        - E1 - Chỉnh sửa hồ sơ của người dùng khác.
2. Biến đầu vào: Họ Tên
    - Lớp hợp lệ: 
        - A2 - Chuỗi ký tự bất kỳ.
    - Lớp không hợp lệ: Không nêu trong đặc tả.
3. Biến đầu vào: Số điện thoại (Đầu số)
    - Lớp hợp lệ: 
        - A3 - Bắt đầu bằng số `0`.
    - Lớp không hợp lệ: 
        - E2 - Bắt đầu bằng chữ số khác `0`.
4. Biến đầu vào: Số điện thoại (Ký tự)
    - Lớp hợp lệ: 
        - A4 - Chỉ chứa các chữ số từ `0` đến `9`.
    - Lớp không hợp lệ: 
        - E3 - Chứa chữ cái, khoảng trắng hoặc ký tự đặc biệt.
5. Biến đầu vào: Số điện thoại (Độ dài)
    - Lớp hợp lệ: 
        - A5 - Có độ dài từ 10 đến 11 chữ số.
    - Lớp không hợp lệ: 
        - E4a - Độ dài dưới 10 chữ số
        - E4b - Độ dài trên 11 chữ số.
6. Biến đầu vào: Địa chỉ giao hàng mặc định
    - Lớp hợp lệ: 
        - A6 - Chuỗi ký tự bất kỳ.
    - Lớp không hợp lệ: Không nêu trong đặc tả.
7. Biến đầu vào: Email
    - Lớp hợp lệ: 
        - A7 - Ở trạng thái Read-only/Disabled trên UI.
    - Lớp không hợp lệ: 
        - E5 - Cố tình can thiệp gửi field Email qua request API.
8. Biến đầu vào: Role (Quyền hạn)
    - Lớp hợp lệ: 
        - A8 - Trạng thái giữ nguyên, không thể thay đổi.
    - Lớp không hợp lệ: 
        - E6 - Cố tình can thiệp gửi field Role qua request API.

| Biến đầu vào / Thuộc tính | Lớp hợp lệ (Valid) | Lớp không hợp lệ (Invalid) |
| :--- | :--- | :--- |
| **Quyền sở hữu hồ sơ** | (A1) Hồ sơ của chính tài khoản đăng nhập | (E1) Cố tình can thiệp hồ sơ người khác |
| **Họ Tên** | (A2) Chuỗi ký tự bất kỳ | Không nêu trong đặc tả |
| **SĐT (Đầu số)** | (A3) Bắt đầu bằng số `0` | (E2) Bắt đầu bằng số khác `0` |
| **SĐT (Ký tự)** | (A4) Chỉ chứa các chữ số `0-9` | (E3) Chứa chữ cái, ký tự đặc biệt |
| **SĐT (Độ dài)** | (A5) Độ dài từ 10 đến 11 chữ số | (E4a) Dưới 10 số<br>(E4b) Trên 11 số |
| **Địa chỉ giao hàng** | (A6) Chuỗi ký tự bất kỳ | Không nêu trong đặc tả |
| **Email** | (A7) Read-only trên giao diện | (E5) Can thiệp Email qua API |
| **Role (Quyền hạn)** | (A8) Không thể thay đổi | (E6) Can thiệp Role qua API |

### 2. Phân tích Giá trị biên (Boundary Value Analysis)
Biến định lượng duy nhất được đề cập trong yêu cầu là **độ dài của số điện thoại** (từ 10 đến 11 chữ số). 

1. Biến định lượng: Độ dài của Số điện thoại
   - Dựa theo đặc tả hệ thống, số điện thoại hợp lệ bắt buộc phải có độ dài nằm trong khoảng "từ 10 đến 11 chữ số". 
   - Từ đó, ta xác định được ranh giới hợp lệ dưới cùng (Min) là `10` chữ số và ranh giới hợp lệ trên cùng (Max) là `11` chữ số.
   - Áp dụng công thức BVA để thiết kế các giá trị ranh giới không hợp lệ nằm ngay sát biên (Min - 1 và Max + 1), ta trích xuất được các giá trị kiểm thử tương ứng là: `9` chữ số (Invalid) và `12` chữ số (Invalid).

| Biến định lượng | Min - 1 | Min | Max | Max + 1 |
| :--- | :--- | :--- | :--- | :--- |
| **Độ dài SĐT** | 9 chữ số (Invalid) | 10 chữ số (Valid) | 11 chữ số (Valid) | 12 chữ số (Invalid) |

### 3. Kịch bản kiểm thử (Test Cases)
Để tối ưu hóa quá trình kiểm thử và tránh trùng lặp kịch bản, các Test Case của Domain Testing và BVA được tổng hợp chung lại thành bảng sau:

| Test Case ID | Title | Pre-conditions | Steps | Expected Results | Actual Result / Note | Verdict |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_FR04_01** | Cập nhật thành công với số điện thoại 10 số (Biên Min) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Thay đổi Họ Tên hợp lệ (Ví dụ: `ABC`).<br>2. Nhập Số điện thoại gồm 10 chữ số và bắt đầu bằng số 0 (Ví dụ: `0123456789`).<br>3. Thay đổi Địa chỉ giao hàng mặc định (Ví dụ: `Nguyen Van Cu 101`).<br>4. Nhấn nút "Cập nhật". | - Hệ thống lưu thông tin thành công<br>- Hiển thị thông báo cập nhật hồ sơ thành công. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_02** | Cập nhật thành công với số điện thoại 11 số (Biên Max) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại gồm 11 chữ số và bắt đầu bằng số 0 (Ví dụ: `01234567890`).<br>2. Nhấn nút "Cập nhật". | - Hệ thống lưu thông tin thành công<br>- Hiển thị thông báo cập nhật hồ sơ thành công. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_03** | Báo lỗi khi số điện thoại có độ dài thấp hơn giới hạn (Biên Min-1) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại gồm 9 chữ số và bắt đầu bằng số 0 (Ví dụ: `012345678`).<br>2. Nhấn nút "Cập nhật". | Hệ thống hiển thị thông báo lỗi SĐT không hợp lệ (độ dài yêu cầu từ 10-11 chữ số) và không cho phép lưu thay đổi. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_04** | Báo lỗi khi số điện thoại có độ dài vượt quá giới hạn (Biên Max+1) | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại gồm 12 chữ số và bắt đầu bằng số 0 (Ví dụ: `012345678901`).<br>2. Nhấn nút "Cập nhật". | Hệ thống hiển thị thông báo lỗi SĐT không hợp lệ hoặc tự động chặn không cho phép nhập ký tự thứ 12 và không tiến hành lưu dữ liệu. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_05** | Báo lỗi khi số điện thoại không bắt đầu bằng số 0 | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại hợp lệ về độ dài (10 hoặc 11 số) nhưng bắt đầu bằng ký tự khác số 0 (Ví dụ: `8412345678`).<br>2. Nhấn nút "Cập nhật". | Hệ thống hiển thị thông báo lỗi yêu cầu số điện thoại phải bắt đầu bằng số 0 và không tiến hành lưu dữ liệu. | Hệ thống thông báo "Cập nhật thành công!" và dữ liệu lưu vào hệ thống | Fail |
| **TC_FR04_06** | Kiểm tra lỗi SĐT chứa ký tự chữ cái hoặc ký tự đặc biệt | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Nhập Số điện thoại có chứa chữ cái/ký tự đặc biệt (VD: `0123abc789` hoặc `0123-456-789`).<br>3. Nhấn nút "Cập nhật". | Giao diện chặn không cho nhập ký tự lạ hoặc hệ thống báo lỗi:<br>- "Số điện thoại chỉ được chứa các chữ số"<br>- "Số điện thoại chứa ký tự không hợp lệ"<br><br>và không tiến hành lưu dữ liệu. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_07** | Báo lỗi khi bỏ trống trường Số điện thoại | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Xóa trắng toàn bộ dữ liệu hiện có trong trường "Số điện thoại".<br>2. Đảm bảo các trường thông tin khác (Họ Tên, Địa chỉ) đều hợp lệ.<br>3. Nhấn nút "Cập nhật". | Giao diện hiển thị thông báo lỗi rõ ràng (Ví dụ: "Số điện thoại không được để trống") và không tiến hành lưu dữ liệu. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và dữ liệu không được lưu. | Fail |
| **TC_FR04_08** | Xác nhận trường Email ở trạng thái không thể chỉnh sửa | Người dùng đã đăng nhập thành công và đang ở giao diện Quản lý hồ sơ cá nhân. | 1. Di chuyển chuột hoặc nhấn vào ô nhập liệu của trường "Email".<br>2. Thử thực hiện thao tác xóa, nhập đè hoặc thay đổi nội dung ký tự trong ô Email. | Trường dữ liệu Email ở trạng thái Read-only hoặc Disabled. Người dùng không thể thực hiện bất kỳ thao tác chỉnh sửa nào trên giao diện. | Trường dữ liệu Email ở trạng thái Read-only, không thể thực hiện thao tác chỉnh sửa nào | Pass |
| **TC_FR04_09** | Không thể tự ý thay đổi thuộc tính Role | Người dùng đang đăng nhập với tài khoản có vai trò (Role) hiện tại là "user". | 1. Mở DevTools (F12) > tab **Network** trên trình duyệt.<br>2. Thực hiện cập nhật hồ sơ hợp lệ trên UI để bắt request cập nhật.<br>3. Trích xuất **JWT Token** tại mục `Authorization: Bearer <token>` trong Request Headers.<br>4. Mở công cụ **Postman**, tạo một request PUT để cập nhật (`http://localhost:3000/api/users/me`).<br>5. Tại tab **Authorization**, chọn **Bearer Token** và dán JWT Token vừa lấy được vào mục **Token**.<br>6. Tại tab **Body** (chọn raw > JSON), dán Payload và cố tình chèn thêm role (Ví dụ: `"role": "admin"`).<br>7. Nhấn **Send** và gọi lại API GET Profile (`http://localhost:3000/api/users/me`) để kiểm tra vai trò hiện tại. | - Hệ thống loại bỏ/bỏ qua tham số `role` không hợp lệ trong request cập nhật hồ sơ.<br>- Thông tin cập nhật các trường khác vẫn thành công nhưng vai trò tài khoản vẫn giữ nguyên là "user". | Sau khi thực hiện lệnh PUT (`http://localhost:3000/api/users/me`) cùng với tham số `role`, hệ thống thông báo đã cập nhật thành công, thông tin được cập nhật và vai trò của tài khoản đổi thành "admin" (trước đó là "user") | Fail |
| **TC_FR04_10** | Không thể cập nhật hồ sơ của tài khoản khác | Hệ thống hiện có tài khoản User A và User B. User A đang thực hiện đăng nhập. | 1. Sử dụng công cụ Developer Tools hoặc Proxy (như Burp Suite) để bắt request cập nhật hồ sơ.<br>2. Thay đổi định danh tài khoản (User ID) trong payload của request từ ID của User A sang ID của User B.<br>3. Gửi request lên server. | Hệ thống từ chối xử lý request, trả về mã lỗi bảo mật (Ví dụ: 403 Forbidden hoặc 401 Unauthorized) và hồ sơ của User B không bị thay đổi. | Hệ thống tự động bỏ qua user ID giả mạo, vì backend xác thực bằng JWT chứ không dựa vào trường `userId` từ phía client gửi | Pass |

### 4. AI Gap Analysis
AI đã bao phủ đúng các case chính của FR-04 như cập nhật hồ sơ hợp lệ, kiểm tra biên độ dài SĐT, kiểm tra Email read-only và kiểm tra không được đổi role. Tuy nhiên:

1. Thiếu test case cho SĐT chứa chữ cái/ký tự đặc biệt. Đây là miền không hợp lệ riêng theo quy tắc "chỉ chứa chữ số", nên không thể thay thế bằng test case kiểm tra độ dài.
2. Thiếu test case cho SĐT bị để trống. Đây là input invalid phổ biến nhưng AI không suy ra được vì trong đặc tả không nêu rõ ràng SĐT là trường bắt buộc.
3. Có một test case sửa `userId` để cập nhật hồ sơ tài khoản khác không phù hợp với hệ thống thật, vì backend xác thực bằng JWT trong header chứ không dựa vào `userId` do client gửi.

Nguyên nhân chính của các thiếu sót này là xuất phát từ việc AI chỉ phân tích dựa trên bề mặt văn bản, AI thường có xu hướng ưu tiên biên độ dài hơn các lớp tương đương chi tiết, đồng thời, AI chưa có context về backend nên đã sinh ra một test case bảo mật không khả thi. Bản tinh chỉnh FR-04 cuối cùng đã khắc phục bằng cách bổ sung kiểm tra ký tự (`TC_FR04_06`), kiểm tra rỗng (`TC_FR04_07`), và loại bỏ (bỏ qua) kịch bản cập nhật chéo tài khoản (`TC_FR04_10`).

### 5. Bug Report
Toàn bộ các bug phát hiện đã được báo cáo chi tiết, bao gồm ảnh chụp minh chứng, mô tả và link dẫn tới Github Issues ở file Bug_Report. 

## Feature 2: FR-07: Giỏ hàng (Shopping Cart)
### 1. Phân tích Miền (Domain Analysis)
Dựa trên đặc tả hệ thống, chức năng Giỏ hàng bao gồm các biến đầu vào và trạng thái chính: Trạng thái giỏ hàng, Thao tác thêm sản phẩm, Thao tác xóa sản phẩm, Nhãn hiển thị tổng tiền và Số lượng sản phẩm.

1. Biến đầu vào: Trạng thái giỏ hàng
    - Lớp hợp lệ: 
        - A1 - Giỏ hàng trống (0 sản phẩm).
        - A2 - Giỏ hàng có sản phẩm (>= 1 sản phẩm).
    - Lớp không hợp lệ: Không có điều kiện loại trừ cụ thể trong context.
2. Biến đầu vào: Thao tác thêm sản phẩm
    - Lớp hợp lệ: 
        - A3 - Thêm một sản phẩm mới hoàn toàn chưa có trong giỏ.
        - A4 - Thêm một sản phẩm đã tồn tại sẵn trong giỏ.
    - Lớp không hợp lệ: Không có điều kiện loại trừ cụ thể trong context.
3. Biến đầu vào: Thao tác xóa sản phẩm
    - Lớp hợp lệ: 
        - A5 - Chọn "Đồng ý/Xác nhận" trên Dialog.
        - A6 - Chọn "Hủy" trên Dialog.
    - Lớp không hợp lệ: 
        - E1 - Sản phẩm bị xóa ngay lập tức mà không có Dialog xác nhận.
4. Biến đầu vào: Nhãn hiển thị tổng tiền
    - Lớp hợp lệ: 
        - A7 - Hiển thị chính xác chuỗi "Tổng cộng".
    - Lớp không hợp lệ: 
        - E2 - Hiển thị chuỗi "Tổng tạm tính".
        - E3 - Hiển thị bất kỳ chuỗi nào khác không phải "Tổng cộng".
5. Biến đầu vào: Số lượng sản phẩm (Quantity)
    - Lớp hợp lệ: 
        - A8 - Giá trị số nguyên >= 1.
    - Lớp không hợp lệ: 
        - E4 - Giá trị = 0.
        - E5 - Giá trị là số âm (VD: -1, -5).

| Biến đầu vào / Thuộc tính | Lớp hợp lệ (Valid) | Lớp không hợp lệ (Invalid) |
| :--- | :--- | :--- |
| **Trạng thái giỏ hàng** | (A1) Giỏ hàng trống<br>(A2) Giỏ hàng có >= 1 sản phẩm | Không có |
| **Thao tác thêm sản phẩm** | (A3) Thêm SP chưa có trong giỏ<br>(A4) Thêm SP đã có trong giỏ | Không có |
| **Thao tác xóa sản phẩm** | (A5) Xác nhận "Đồng ý" trên Dialog<br>(A6) Xác nhận "Hủy" trên Dialog | (E1) Bỏ qua Dialog xác nhận |
| **Nhãn tổng tiền** | (A7) Hiển thị "Tổng cộng" | (E2) Hiển thị "Tổng tạm tính"<br>(E3) Nhãn bất kỳ khác |
| **Số lượng sản phẩm** | (A8) Giá trị >= 1 | (E4) Giá trị = 0<br>(E5) Giá trị số âm |

### 2. Phân tích Giá trị biên (Boundary Value Analysis)
Biến định lượng duy nhất được xác định trong context là **số lượng (Quantity)** của một sản phẩm trong giỏ hàng (thao tác thông qua nút +/-). Do context không quy định giới hạn tối đa (Max), các giá trị biên chỉ được áp dụng cho giới hạn tối thiểu (Min = 1).

1. Biến định lượng: Số lượng của một sản phẩm (Quantity)
   - Theo logic nghiệp vụ thông thường của giỏ hàng và đặc tả (điều chỉnh qua nút +/-), một sản phẩm khi đã tồn tại trong giỏ thì số lượng tối thiểu phải là 1. Do đó, ranh giới hợp lệ dưới cùng (Min) được xác định là `1`.
   - Đặc tả hiện tại không quy định giới hạn số lượng tối đa (Max) mà một người dùng có thể mua cho một mặt hàng, nên ranh giới trên tạm thời được xem là Không xác định (N/A).
   - Áp dụng công thức BVA cho ranh giới dưới (Min-1, Min), ta trích xuất được các giá trị kiểm thử: `0` (Invalid) và `1` (Valid).

| Biến định lượng | Min - 1 | Min | Max | Max + 1 |
| :--- | :--- | :--- | :--- | :--- |
| **Số lượng của một sản phẩm** | 0 (Invalid) | 1 (Valid) | N/A | N/A |

### 3. Kịch bản kiểm thử (Test Cases)
Để tối ưu hóa quá trình kiểm thử và tránh trùng lặp kịch bản, các Test Case của Domain Testing và BVA được tổng hợp chung lại thành bảng sau:

| Test Case ID | Title | Pre-conditions | Steps | Expected Results | Actual Result / Note | Verdict |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_FR07_01** | Kiểm tra hiển thị khi giỏ hàng trống | Người dùng truy cập vào giỏ hàng và chưa chọn mua bất kỳ sản phẩm nào. | 1. Đi đến trang Giỏ hàng. | - Hiển thị hình minh họa giỏ hàng trống.<br>- Hiển thị thông báo rõ ràng về trạng thái giỏ hàng trống. | Khi giỏ hàng đang trống, trang chỉ hiển thị thông báo "Giỏ hàng của bạn đang trống" khi vào trang, không có hình minh họa | Fail |
| **TC_FR07_02** | Kiểm tra hiển thị danh sách các cột khi có sản phẩm | Giỏ hàng đã có ít nhất một sản phẩm. | 1. Đi đến trang Giỏ hàng.<br>2. Kiểm tra các cột trong bảng danh sách sản phẩm. | - Hiển thị danh sách sản phẩm với đầy đủ các cột: Sản phẩm, Đơn giá, Số lượng, Thành tiền, Thao tác.<br>- Cột Số lượng phải có nút `+` và `-` để chỉnh sửa. | Khi vào giỏ hàng (có 1 sản phẩm), hệ thống hiển thị các cột: Sản phẩm, Giá, Số lượng, Thành tiền, Thao tác (có thao tác `Xóa`). Nhưng cột Số lượng không có nút `+` và nút `-` để chỉnh sửa số lượng. | Fail |
| **TC_FR07_03** | Kiểm tra nhãn hiển thị của Tổng tiền | Giỏ hàng đang có sản phẩm. | 1. Đi đến trang Giỏ hàng.<br>2. Quan sát phần hiển thị tổng số tiền phải thanh toán. | - Nhãn hiển thị chính xác từ: "Tổng cộng".<br>- KHÔNG hiển thị từ "Tổng tạm tính". | Hiển thị chính xác số tiền của giỏ hàng, nhưng nhãn hiển thị từ: "Tổng tạm tính" chứ không phải "Tổng cộng" | Fail |
| **TC_FR07_04** | Kiểm tra thêm cùng một sản phẩm đã có trong giỏ hàng | Giỏ hàng đang có sản phẩm A với Số lượng là 1. | 1. Quay lại trang danh sách sản phẩm.<br>2. Thực hiện thêm sản phẩm A vào giỏ một lần nữa.<br>3. Đi đến trang Giỏ hàng kiểm tra. | - Hệ thống không tạo thêm dòng mới cho sản phẩm A.<br>- Số lượng của sản phẩm A tăng lên thành 2.<br>- Giá trị Thành tiền và Tổng cộng được cập nhật tăng tương ứng. | Sau khi thêm lại sản phẩm A vào giỏ, hệ thống tạo thêm dòng mới chứ không tăng số lượng của sản phẩm A thành 2. | Fail |
| **TC_FR07_05** | Kiểm tra tăng số lượng sản phẩm bằng nút [+] | Giỏ hàng đang có sản phẩm A với Số lượng là 1. | 1. Đi đến trang Giỏ hàng.<br>2. Nhấn vào nút `+` tại cột Số lượng của sản phẩm A. | - Số lượng sản phẩm A tăng lên thành 2.<br>- Giá trị Thành tiền và Tổng cộng tự động cập nhật chính xác. | Giao diện không có nút `+` để thực hiện test case, nên không thể thực hiện | Skip |
| **TC_FR07_06** | Kiểm tra giảm số lượng sản phẩm bằng nút [-] (Giá trị Min) | Giỏ hàng đang có sản phẩm A với Số lượng là 2. | 1. Đi đến trang Giỏ hàng.<br>2. Nhấn vào nút `-` tại cột Số lượng của sản phẩm A để giảm về 1. | - Số lượng sản phẩm A giảm xuống còn 1 (Giá trị Min).<br>- Giá trị Thành tiền và Tổng cộng tự động cập nhật chính xác. | Giao diện không có nút `-` để thực hiện test case, nên không thể thực hiện | Skip |
| **TC_FR07_07** | Kiểm tra nhấn nút [-] khi số lượng đang ở mức tối thiểu (Giá trị Biên Min - 1) | Giỏ hàng đang có sản phẩm A với Số lượng là 1. | 1. Đi đến trang Giỏ hàng.<br>2. Nhấn vào nút `-` tại cột Số lượng của sản phẩm A. | - Hệ thống không cho phép giảm số lượng xuống 0 (Hoặc hiển thị dialog xác nhận xóa sản phẩm tùy theo hành vi xử lý biên của hệ thống). | Giao diện không có nút `-` để thực hiện test case, nên không thể thực hiện | Skip |
| **TC_FR07_08** | Kiểm tra hủy thao tác xóa sản phẩm qua Dialog xác nhận | Giỏ hàng đang có sản phẩm A. | 1. Đi đến trang Giỏ hàng.<br>2. Nhấn vào nút Xóa tại cột Thao tác của sản phẩm A.<br>3. Trên Dialog xác nhận xuất hiện, nhấn nút "Hủy". | - Xuất hiện Dialog xác nhận trước khi thực hiện xóa.<br>- Khi nhấn "Hủy", Dialog đóng lại.<br>- Sản phẩm A không bị xóa và vẫn giữ nguyên trong giỏ hàng. | Sau khi ấn nút `Xóa` tại cột Thao tác của sản phẩm A, sản phẩm A bị xóa ngay lập tức mà không có Dialog xác nhận | Fail |
| **TC_FR07_09** | Kiểm tra đồng ý xóa sản phẩm qua Dialog xác nhận | Giỏ hàng đang có sản phẩm A. | 1. Đi đến trang Giỏ hàng.<br>2. Nhấn vào nút Xóa tại cột Thao tác của sản phẩm A.<br>3. Trên Dialog xác nhận xuất hiện, nhấn nút "Đồng ý/Xác nhận". | - Xuất hiện Dialog xác nhận trước khi thực hiện xóa.<br>- Khi nhấn "Đồng ý/Xác nhận", Dialog đóng lại.<br>- Sản phẩm A bị xóa hoàn toàn khỏi danh sách giỏ hàng.<br>- Giá trị Tổng cộng được tính toán lại chính xác. | Sau khi ấn nút `Xóa` tại cột Thao tác của sản phẩm A, sản phẩm A bị xóa ngay lập tức mà không có Dialog xác nhận | Fail |
| **TC_FR07_10** | Kiểm tra chức năng của nút "Tiếp tục mua sắm" | Người dùng đang ở trang Giỏ hàng và giỏ hàng đang trống. | 1. Nhấn vào nút "Tiếp tục mua sắm". | - Hệ thống điều hướng người dùng quay trở về Trang chủ một cách chính xác. | Sau khi nhấn nút vào nút "Tiếp tục mua sắm", hệ thống điều hướng người dùng quay trở về Trang chủ | Pass |
| **TC_FR07_11** | Kiểm tra chức năng của nút "Mua tiếp" | Người dùng đang ở trang Giỏ hàng và giỏ hàng đang có một sản phẩm. | 1. Nhấn vào nút "← Mua tiếp". | - Hệ thống điều hướng người dùng quay trở về Trang chủ một cách chính xác. | Sau khi nhấn nút vào nút "Mua tiếp", hệ thống điều hướng người dùng quay trở về Trang chủ | Pass |
| **TC_FR07_12** | Kiểm tra tính nhất quán trạng thái của giỏ hàng | Người dùng đang ở trang Giỏ hàng và giỏ hàng đang có một sản phẩm. | 1. Nhấn nút refresh trên thanh công cụ (hoặc F5) | Giỏ hàng phải giữ nguyên trạng thái và số lượng các sản phẩm như trước khi Refresh trang. | Sau khi nhấn nút refresh trang (F5), giỏ hàng mất hết toàn bộ sản phẩm, biến thành giỏ hàng trống. | Fail |
| **TC_FR07_13** | Kiểm tra hệ thống có cho phép số lượng sản phẩm là số âm | Người dùng đang ở trang chi tiết Sản phẩm bất kỳ và giỏ hàng đang trống. | 1. Nhập số âm bất kỳ vào mục Số lượng ở trang chi tiết Sản phẩm (Ví dụ: `-5`)<br>2. Nhấn nút "Thêm vào giỏ hàng" | - Hệ thống phải từ chối hoặc ngăn chặn người dùng thêm vào ở giao diện, phải có thông báo rõ ràng cho người dùng biết.<br>- Hoặc khi người dùng nhập dấu trừ `-` ô nhập liệu phải chặn hoặc tự động khôi phục giá trị về số `1`. | Hệ thống chấp nhận số lượng âm và đưa vào Giỏ hàng bình thường, cột Thành tiền và Tổng cộng bị tính ra số âm. | Fail |

### 4. AI Gap Analysis
AI đã bao phủ các luồng chính của FR-07 như trạng thái giỏ hàng trống, hiển thị danh sách sản phẩm, nhãn tổng tiền và thao tác xóa/thêm sản phẩm. Tuy nhiên vẫn còn các thiếu sót sau:

1. AI gộp chung thao tác tăng và giảm số lượng vào một test case, làm giảm tính độc lập của kiểm thử và em đã tách thành `TC_FR07_05` và `TC_FR07_06`.
2. Thiếu test case kiểm tra mất dữ liệu khi refresh trang (F5). Đây là lỗi trạng thái rất phổ biến của giỏ hàng nhưng prompt ban đầu thiên về giao diện nên AI không suy ra được.
3. Thiếu test case cho số lượng sản phẩm âm từ trang chi tiết sản phẩm mà chỉ bám vào luồng trong giỏ hàng. Nên không phát hiện được input bất thường ở màn hình khác.
4. Thiếu test case `TC_FR07_11: Kiểm tra chức năng của nút "Mua tiếp"` vì nút này không được nêu trong đặc tả ban đầu, mặc dù là trong thực tế có trên giao diện.

(Bên cạnh đó có một số test case như `TC_FR07_05`, `TC_FR07_06`, `TC_FR07_07` không thể thực hiện được do source code không như đặc tả, nút `+`/`-` không hề tồn tại trong cột Số lượng mặc dù đặc tả có ghi)

Nguyên nhân chính của các thiếu sót này là AI ưu tiên các kiểm thử phần "bề mặt" trong UI thay vì các tình huống trạng thái và kiểm thử xuyên màn hình. Bản tinh chỉnh FR-07 đã khắc phục bằng cách tách kiểm thử số lượng thành hai case riêng và bổ sung thêm `TC_FR07_11`, `TC_FR07_12`, `TC_FR07_13` để đảm bảo bao phủ đầy đủ hơn.

### 5. Bug Report
Toàn bộ các bug phát hiện đã được báo cáo chi tiết, bao gồm ảnh chụp minh chứng, mô tả và link dẫn tới Github Issues ở file Bug_Report. 

## Feature 3: FR-15: Product management (CRUD)
### 1. Phân tích Miền (Domain Analysis)
Dựa trên đặc tả hệ thống, chức năng Quản lý sản phẩm bao gồm 3 biến đầu vào chính: Tên sản phẩm, Giá và Danh mục.

1. Biến đầu vào: Tên sản phẩm
    - Lớp hợp lệ: 
        - A1 - Chứa từ 1 đến 255 ký tự.
    - Lớp không hợp lệ: 
        - E1 - Để trống (0 ký tự).
        - E2 - Vượt quá 255 ký tự.
2. Biến đầu vào: Giá
    - Lớp hợp lệ: 
        - A2 - Giá trị là số dương (> 0).
    - Lớp không hợp lệ: 
        - E3 - Để trống.
        - E4 - Số bằng 0.
        - E5 - Số âm (< 0).
        - E6 - Chứa ký tự đặc biệt (không phải số).
3. Biến đầu vào: Danh mục
    - Lớp hợp lệ: 
        - A3 - Một danh mục hợp lệ được chọn từ danh sách có sẵn.
    - Lớp không hợp lệ: 
        - E7 - Để trống (không chọn danh mục nào).

| Biến đầu vào / Thuộc tính | Lớp hợp lệ (Valid) | Lớp không hợp lệ (Invalid) |
| :--- | :--- | :--- |
| **Tên sản phẩm** | (A1) Chứa từ 1 - 255 ký tự | (E1) Để trống<br>(E2) Vượt quá 255 ký tự |
| **Giá** | (A2) Giá trị số dương (> 0) | (E3) Để trống<br>(E4) Bằng 0<br>(E5) Số âm<br>(E6) Chứa ký tự không phải số |
| **Danh mục** | (A3) Chọn 1 danh mục có sẵn | (E7) Để trống (Không chọn) |

### 2. Phân tích Giá trị biên (Boundary Value Analysis)
Đối với chức năng này, có 2 biến định lượng cần áp dụng phân tích giá trị biên là **Chiều dài Tên sản phẩm** (từ 1 đến 255 ký tự) và **Giá sản phẩm** (số dương > 0, mặc định ranh giới dưới là 1 đối với số nguyên).

1. Biến định lượng 1: Chiều dài Tên sản phẩm
   - Đặc tả yêu cầu bắt buộc nhập và tối đa 255 ký tự. Do đó, ranh giới hợp lệ là từ 1 đến 255 ký tự.
   - Áp dụng BVA (Min-1, Min, Max, Max+1), ta có các giá trị kiểm thử: `0` (Invalid - để trống), `1` (Valid), `255` (Valid), và `256` (Invalid).

2. Biến định lượng 2: Giá sản phẩm
   - Đặc tả yêu cầu giá phải là số dương (> 0). Giả định hệ thống áp dụng cho tiền tệ Việt Nam (VNĐ) không dùng số thập phân, ranh giới dưới tối thiểu (Min) sẽ là `1`. Không có giới hạn trên (Max) được quy định.
   - Áp dụng BVA cho ranh giới dưới, ta có các giá trị kiểm thử: `0` (Invalid) và `1` (Valid).

| Biến định lượng | Min - 1 | Min | Max | Max + 1 |
| :--- | :---: | :---: | :---: | :---: |
| **Chiều dài Tên sản phẩm** (ký tự) | 0 (Invalid) | 1 (Valid) | 255 (Valid) | 256 (Invalid) |
| **Giá sản phẩm** (giá trị số) | 0 (Invalid) | 1 (Valid) | N/A | N/A |

### 3. Kịch bản kiểm thử (Test Cases)
Để tối ưu hóa quá trình kiểm thử và tránh trùng lặp kịch bản, các Test Case của Domain Testing và BVA được tổng hợp chung lại thành bảng sau:

| Test Case ID | Title | Pre-conditions | Steps | Expected Results | Actual Result / Note | Verdict |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_FR15_01** | Sản phẩm mới với Tên sản phẩm ở biên Min (1 ký tự) | Đăng nhập với quyền Admin và đang ở trang Sản phẩm. | 1. Nhập Tên sản phẩm: "A" (1 ký tự)<br>2. Nhập Giá: 1000<br>3. Chọn Danh mục hợp lệ<br>4. Nhập URL ảnh hợp lệ (Ví dụ: `https://placehold.co/300x300/png?text=iPhone+15`)<br>5. Nhấn "Lưu sản phẩm" | - Hệ thống lưu thành công.<br>- Sản phẩm "A" hiển thị trong danh sách với đúng thông tin. | - Hệ thống lưu thành công sản phẩm.<br>- Sản phẩm "A" hiển thị trong danh sách với đúng thông tin. | Pass |
| **TC_FR15_02** | Sản phẩm mới với Tên sản phẩm ở biên Max (255 ký tự) | Đăng nhập với quyền Admin và đang ở trang Sản phẩm. | 1. Nhập Tên sản phẩm: Chuỗi ngẫu nhiên đúng 255 ký tự<br>2. Nhập Giá: 5000<br>3. Chọn Danh mục hợp lệ<br>4. Nhập URL ảnh hợp lệ (Ví dụ: `https://placehold.co/300x300/png?text=iPhone+15`)<br>5. Nhấn "Lưu sản phẩm" | - Hệ thống lưu thành công.<br>- Sản phẩm hiển thị trong danh sách mà không bị cắt xén tên. | - Hệ thống lưu sản phẩm thành công.<br>- Sản phẩm được hiển thị sau khi thêm vào và không bị cắt xén tên. | Pass |
| **TC_FR15_03** | Báo lỗi khi Tên sản phẩm trống (Min - 1) | Đăng nhập với quyền Admin và đang ở trang Sản phẩm. | 1. Để trống Tên sản phẩm<br>2. Nhập Giá: 1000<br>3. Chọn Danh mục hợp lệ<br>4. Nhập URL ảnh hợp lệ (Ví dụ: `https://placehold.co/300x300/png?text=iPhone+15`)<br>5. Nhấn "Lưu sản phẩm" | Hệ thống chặn hành động lưu và hiển thị thông báo lỗi bắt buộc nhập Tên sản phẩm. | Hệ thống chặn hành động lưu sản phẩm và hiển thị thông báo lỗi bắt buộc nhập trường Tên sản phẩm. | Pass |
| **TC_FR15_04** | Báo lỗi khi Tên sản phẩm vượt quá 255 ký tự (Max + 1) | Đăng nhập với quyền Admin và đang ở trang Sản phẩm. | 1. Nhập Tên sản phẩm: Chuỗi ngẫu nhiên 256 ký tự<br>2. Nhập Giá: 1000<br>3. Chọn Danh mục hợp lệ<br>4. Nhập URL ảnh hợp lệ (Ví dụ: `https://placehold.co/300x300/png?text=iPhone+15`)<br>5. Nhấn "Lưu sản phẩm" | Hệ thống chặn hành động lưu và hiển thị thông báo lỗi vượt quá giới hạn 255 ký tự. | Hệ thống không chặn mà lưu sản phẩm vào hệ thống mặc dù đã trên 255 ký tự. | Fail |
| **TC_FR15_05** | Báo lỗi khi Giá sản phẩm bằng 0 (Biên Min - 1) | Đăng nhập với quyền Admin và đang ở trang Sản phẩm. | 1. Nhập Tên sản phẩm hợp lệ<br>2. Nhập Giá: 0<br>3. Chọn Danh mục hợp lệ<br>4. Nhập URL ảnh hợp lệ (Ví dụ: `https://placehold.co/300x300/png?text=iPhone+15`)<br>5. Nhấn "Lưu sản phẩm" | Hệ thống chặn hành động lưu và hiển thị thông báo lỗi giá phải lớn hơn 0. | Hệ thống không chặn mà lưu sản phẩm vào hệ thống mặc dù giá hiện đang là `0`. | Fail |
| **TC_FR15_06** | Báo lỗi khi Giá sản phẩm là số âm | Đăng nhập với quyền Admin và đang ở trang Sản phẩm. | 1. Nhập Tên sản phẩm hợp lệ<br>2. Nhập Giá là 1 số âm (Ví dụ: `-1`)<br>3. Chọn Danh mục hợp lệ<br>4. Nhập URL ảnh hợp lệ (Ví dụ: `https://placehold.co/300x300/png?text=iPhone+15`)<br>5. Nhấn "Lưu sản phẩm" | Hệ thống chặn hành động lưu và hiển thị thông báo lỗi giá phải lớn hơn 0. | Hệ thống không chặn mà lưu sản phẩm vào hệ thống mặc dù giá hiện đang là số âm (`-1`). | Fail |
| **TC_FR15_07** | Báo lỗi khi bỏ trống Giá sản phẩm | Đăng nhập với quyền Admin và đang ở trang Sản phẩm. | 1. Nhập Tên sản phẩm hợp lệ<br>2. Bỏ trống trường Giá<br>3. Chọn Danh mục hợp lệ<br>4. Nhập URL ảnh hợp lệ (Ví dụ: `https://placehold.co/300x300/png?text=iPhone+15`)<br>5. Nhấn "Lưu sản phẩm" | Hệ thống chặn hành động lưu và hiển thị thông báo lỗi giá phải lớn hơn 0. | Hệ thống không chặn mà lưu sản phẩm vào hệ thống mặc dù giá hiện đang bỏ trống. | Fail |
| **TC_FR15_08** | Báo lỗi/ngăn chặn khi nhập ký tự không phải số vào Giá sản phẩm | Đăng nhập với quyền Admin và đang ở trang Sản phẩm. | 1. Nhập Tên sản phẩm hợp lệ<br>2. Nhập Giá có chứa ký tự không phải số (Ví dụ: `123abc`)<br>3. Chọn Danh mục hợp lệ<br>4. Nhập URL ảnh hợp lệ (Ví dụ: `https://placehold.co/300x300/png?text=iPhone+15`)<br>5. Nhấn "Lưu sản phẩm" | - Hệ thống chặn hành động lưu và hiển thị thông báo lỗi giá không được phép chứa ký tự không phải số.<br>- Hoặc là hệ thống chặn lại không cho nhập các ký tự khác số. | Hệ thống chặn lại các ký tự không phải số (Khi nhập `123abc` chỉ `123` được nhập vào trường Giá sản phẩm). | Pass |
| **TC_FR15_09** | Báo lỗi khi không chọn Danh mục | Đăng nhập với quyền Admin, đã xóa hết toàn bộ danh mục trong trang "Danh mục" và đang ở trang Sản phẩm. | 1. Nhập Tên sản phẩm hợp lệ<br>2. Nhập Giá: 1000<br>3. Không chọn Danh mục<br>4. Nhập URL ảnh hợp lệ (Ví dụ: `https://placehold.co/300x300/png?text=iPhone+15`)<br>5. Nhấn "Lưu sản phẩm" | Hệ thống chặn hành động lưu và hiển thị thông báo lỗi bắt buộc chọn danh mục. | Hệ thống không chặn hành động lưu mà lưu sản phẩm bị trống phần danh mục vào trong hệ thống. | Fail |
| **TC_FR15_10** | Kiểm tra hiển thị nút có chức năng Xem chi tiết | Đăng nhập với quyền Admin, có sẵn ít nhất 1 sản phẩm và đang ở trang Sản phẩm. | 1. Kiểm tra các cột ở danh sách các sản phẩm | - Phải tồn tại nút có nội dung "Xem chi tiết".<br>- Hoặc khi nhấn vào biểu tượng sản phẩm, Admin phải xem được thông tin chi tiết của sản phẩm. | - Không tồn tại nút hay bất kỳ cách nào để xem chi tiết sản phẩm.<br> - Chỉ có thể xem thông tin chi tiết của sản phẩm (đầy đủ tên sản phẩm, giá, URL ảnh, mô tả và danh mục) thông qua nút "Sửa". | Fail |
| **TC_FR15_11** | Xem chi tiết một sản phẩm | Đăng nhập với quyền Admin, có sẵn ít nhất 1 sản phẩm và đang ở trang Sản phẩm. | 1. Nhấn vào biểu tượng/nút Xem chi tiết của sản phẩm | Hệ thống hiển thị đúng và đầy đủ thông tin: Tên, Giá, Danh mục của sản phẩm được chọn. | Không có biểu tượng/nút Xem chi tiết hay bất kỳ cách nào để có thể xem chi tiết của sản phẩm. | Skip |
| **TC_FR15_12** | Hiển thị ảnh placeholder khi để trống mục URL ảnh | Đăng nhập với quyền Admin và đang ở trang Sản phẩm. | 1. Nhập Tên sản phẩm hợp lệ<br>2. Nhập Giá: 1000<br>3. Chọn Danh mục hợp lệ<br>4. Để trống URL ảnh<br>5. Nhấn "Lưu sản phẩm" | Hệ thống tự động đưa ra 1 ảnh làm placeholder nếu như người dùng không nhập URL ảnh. Hoặc có thuộc tính `alt` để mô tả nội dung ảnh | Hệ thống tuy không đưa ra ảnh làm placeholder nhưng vẫn có text (`alt`) để miêu tả nội dung ảnh. | Pass |
| **TC_FR15_13** | Cập nhật thông tin sản phẩm và kiểm tra tính độc lập | Đăng nhập với quyền Admin và có sẵn Sản phẩm A và B (hoặc các sản phẩm khác). | 1. Chọn Sửa Sản phẩm A<br>2. Đổi Tên và Giá thành giá trị hợp lệ mới<br>3. Nhấn "Lưu sản phẩm"<br>4. Kiểm tra lại Sản phẩm A và B (hoặc các sản phẩm khác) | - Sản phẩm A được cập nhật thông tin mới.<br>- Sản phẩm B không có bất kỳ thay đổi nào (giữ nguyên dữ liệu cũ). | - Tên của toàn bộ sản phẩm bị đổi thành tên của sản phẩm vừa được đổi và giá của sản phẩm bị đổi cũng không được cập nhật.<br>- Tuy nhiên sau khi refresh (F5) trang thì dữ liệu quay lại bình thường, nhưng đây vẫn là bug UI vì trạng thái hiển thị trước đó bị sai. | Fail |
| **TC_FR15_14** | Xóa một sản phẩm khỏi hệ thống | Đăng nhập với quyền Admin và có sẵn một sản phẩm. | 1. Nhấn nút Xóa tại sản phẩm muốn xóa<br>2. Xác nhận Xóa (nếu có popup) | Hệ thống xóa thành công và sản phẩm không còn xuất hiện trong danh sách. | Hệ thống xóa thành công và sản phẩm không còn xuất hiện trong danh sách nữa. | Pass |

### 4. AI Gap Analysis
AI đã bao phủ khá tốt phần kiểm thử dữ liệu cốt lõi của FR-15 như biên độ dài Tên sản phẩm, Giá bằng 0 và Giá âm. Tuy nhiên vẫn còn các thiếu sót sau:

1. Thiếu test case kiểm tra sự tồn tại và hoạt động của nút "Xem chi tiết" trên giao diện danh sách sản phẩm.
2. Bỏ sót trường "URL ảnh" và logic hiển thị ảnh placeholder khi URL bị để trống. Nguyên nhân là AI bám gần như hoàn toàn vào văn bản đặc tả gốc nên không suy ra các trường đã tồn tại trong source code.
3. AI chưa tách đầy đủ các tình huống invalid của trường Giá thành các nhóm độc lập, đặc biệt là trường hợp bỏ trống và trường hợp số âm, nên độ bao phủ chưa hoàn chỉnh ở lớp tương đương.

Nguyên nhân chính của các thiếu sót này là AI quá thiên về lý thuyết Domain/BVA và phụ thuộc vào phần mô tả trong prompt, trong khi không tự kiểm tra được các chi tiết giao diện hoặc dữ liệu thực tế của màn hình. Bản tinh chỉnh FR-15 đã khắc phục bằng cách tách riêng test case của trường Giá (thành `TC_FR15_06`, `TC_FR15_07`), bổ sung `TC_FR15_08`, `TC_FR15_10`, `TC_FR15_12`, đồng thời chuẩn hóa lại bước thao tác lưu sản phẩm để khớp với giao diện thực tế.

### 5. Bug Report
Toàn bộ các bug phát hiện đã được báo cáo chi tiết, bao gồm ảnh chụp minh chứng, mô tả và link dẫn tới Github Issues ở file Bug_Report. 

## Feature 4: FR-20: Hồ sơ cá nhân (FR-04 - Mobile)
### 1. Phân tích Miền (Domain Analysis)
Dựa trên đặc tả hệ thống và đặc thù môi trường di động, chức năng Quản lý hồ sơ cá nhân bao gồm các biến đầu vào và trạng thái chính: Quyền sở hữu hồ sơ, Họ Tên, Số điện thoại, Địa chỉ giao hàng mặc định, Email và Role.

1. Biến đầu vào: Quyền sở hữu hồ sơ
    - Lớp hợp lệ: 
        - A1 - Chỉnh sửa hồ sơ thuộc sở hữu của chính tài khoản đang đăng nhập.
    - Lớp không hợp lệ: 
        - E1 - Chỉnh sửa hồ sơ của người dùng khác.
2. Biến đầu vào: Họ Tên
    - Lớp hợp lệ: 
        - A2 - Chuỗi ký tự bất kỳ.
    - Lớp không hợp lệ: Không nêu trong đặc tả.
3. Biến đầu vào: Số điện thoại (Đầu số)
    - Lớp hợp lệ: 
        - A3 - Bắt đầu bằng chữ số `0`.
    - Lớp không hợp lệ: 
        - E2 - Bắt đầu bằng chữ số khác `0` (Ví dụ: 1-9).
4. Biến đầu vào: Số điện thoại (Ký tự)
    - Lớp hợp lệ: 
        - A4 - Chỉ chứa các chữ số từ `0` đến `9`.
    - Lớp không hợp lệ: 
        - E3 - Chứa chữ cái, khoảng trắng hoặc ký tự đặc biệt.
5. Biến đầu vào: Số điện thoại (Độ dài)
    - Lớp hợp lệ: 
        - A5 - Có độ dài từ 10 đến 11 chữ số.
    - Lớp không hợp lệ: 
        - E4a - Độ dài dưới 10 chữ số
        - E4b - Độ dài trên 11 chữ số.
6. Biến đầu vào: Địa chỉ giao hàng mặc định
    - Lớp hợp lệ: 
        - A6 - Chuỗi ký tự bất kỳ.
    - Lớp không hợp lệ: Không nêu trong đặc tả.
7. Biến đầu vào: Email
    - Lớp hợp lệ: 
        - A7 - Ở trạng thái Read-only trên giao diện (UI).
    - Lớp không hợp lệ: 
        - E5 - Cố ý chèn/thay đổi giá trị Email trong payload gửi lên API.
8. Biến đầu vào: Role (Quyền hạn)
    - Lớp hợp lệ: 
        - A8 - Trạng thái giữ nguyên, không thể thay đổi.
    - Lớp không hợp lệ: 
        - E6 - Có thể thay đổi giá trị thuộc tính Role qua request/giao diện.

| Biến đầu vào / Thuộc tính | Miền hợp lệ (Valid) | Miền không hợp lệ (Invalid) |
| :--- | :--- | :--- |
| **Quyền sở hữu hồ sơ** | (A1) Hồ sơ của chính tài khoản đăng nhập | (E1) Cố tình can thiệp hồ sơ người khác |
| **Họ Tên** | (A2) Chuỗi ký tự bất kỳ | Không nêu trong đặc tả |
| **SĐT (Đầu số)** | (A3) Bắt đầu bằng số `0` | (E2) Bắt đầu bằng số khác `0` |
| **SĐT (Ký tự)** | (A4) Chỉ chứa các chữ số `0-9` | (E3) Chứa chữ cái, ký tự đặc biệt |
| **SĐT (Độ dài)** | (A5) Độ dài từ 10 đến 11 chữ số | (E4a) Dưới 10 số<br>(E4b) Trên 11 số |
| **Địa chỉ giao hàng mặc định** | (A6) Chuỗi ký tự bất kỳ | Không nêu trong đặc tả |
| **Email** | (A7) Read-only trên giao diện | (E5) Can thiệp Email qua API |
| **Role (Quyền hạn)** | (A8) Không thể thay đổi | (E6) Can thiệp Role qua API |

### 2. Phân tích Giá trị biên (Boundary Value Analysis)
Biến định lượng duy nhất được đề cập trong yêu cầu là **độ dài của số điện thoại** (từ 10 đến 11 chữ số).

1. Biến định lượng: Độ dài của Số điện thoại
   - Dựa theo đặc tả hệ thống, số điện thoại hợp lệ bắt buộc phải có độ dài nằm trong khoảng "từ 10 đến 11 chữ số".
   - Từ đó, ta xác định được ranh giới hợp lệ dưới cùng (Min) là `10` chữ số và ranh giới hợp lệ trên cùng (Max) là `11` chữ số.
   - Áp dụng công thức BVA để thiết kế các giá trị ranh giới không hợp lệ nằm ngay sát biên (Min - 1 và Max + 1), ta trích xuất được các giá trị kiểm thử tương ứng là: `9` chữ số (Invalid) và `12` chữ số (Invalid).

| Biến định lượng | Min - 1 | Min | Max | Max + 1 |
| :--- | :--- | :--- | :--- | :--- |
| **Độ dài SĐT** | 9 chữ số (Invalid) | 10 chữ số (Valid) | 11 chữ số (Valid) | 12 chữ số (Invalid) |

### 3. Kịch bản kiểm thử (Test Cases)
Để tối ưu hóa quá trình kiểm thử và tránh trùng lặp kịch bản, các Test Case của Domain Testing và BVA được tổng hợp chung lại thành bảng sau:

| Test Case ID | Title | Pre-conditions | Steps | Expected Results | Actual Result / Note | Verdict |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC_FR20_01** | Cập nhật thành công thông tin với SĐT 10 số (Biên Min) | Người dùng đã đăng nhập vào hệ thống thành công và đang ở màn hình Quản lý hồ sơ cá nhân. | 1. Thay đổi Họ Tên và Địa chỉ hợp lệ.<br>2. Nhập SĐT: `0912345678` (10 chữ số, bắt đầu bằng 0).<br>3. Nhấn nút "Cập nhật". | Hệ thống cập nhật thông tin thành công, hiển thị thông báo thành công và dữ liệu mới được lưu lại. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và không cập nhật thông tin. | Fail |
| **TC_FR20_02** | Cập nhật thành công thông tin với SĐT 11 số (Biên Max) | Người dùng đã đăng nhập vào hệ thống thành công và đang ở màn hình Quản lý hồ sơ cá nhân. | 1. Thay đổi Họ Tên và Địa chỉ hợp lệ.<br>2. Nhập SĐT: `01234567890` (11 chữ số, bắt đầu bằng 0).<br>3. Nhấn nút "Cập nhật". | Hệ thống cập nhật thông tin thành công, hiển thị thông báo thành công và dữ liệu mới được lưu lại. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và không cập nhật thông tin. | Fail |
| **TC_FR20_03** | Báo lỗi khi nhập SĐT có độ dài thấp hơn giới hạn (Biên Min-1) | Người dùng đã đăng nhập thành công và đang ở màn hình Quản lý hồ sơ cá nhân. | 1. Nhập các thông tin khác hợp lệ.<br>2. Nhập SĐT: `012345678` (chỉ có 9 chữ số).<br>3. Nhấn nút "Cập nhật". | Hệ thống chặn lại, hiển thị thông báo lỗi: "Số điện thoại phải từ 10 đến 11 chữ số". Dữ liệu không được lưu. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và không cập nhật thông tin. | Fail |
| **TC_FR20_04** | Báo lỗi khi nhập SĐT có độ dài vượt quá giới hạn (Biên Max+1) | Người dùng đã đăng nhập thành công và đang ở màn hình Quản lý hồ sơ cá nhân. | 1. Nhập các thông tin khác hợp lệ.<br>2. Nhập SĐT: `012345678901` (có 12 chữ số).<br>3. Nhấn nút "Cập nhật". | Hệ thống chặn lại, hiển thị thông báo lỗi: "Số điện thoại phải từ 10 đến 11 chữ số". Dữ liệu không được lưu. | Hệ thống báo lỗi "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số." và không cập nhật thông tin. | Fail |
| **TC_FR20_05** | Layout không bị vỡ sau khi cập nhật thành công thông tin với Họ tên bằng chuỗi 255 ký tự | Người dùng đã đăng nhập thành công và đang ở màn hình Quản lý hồ sơ cá nhân. | 1. Nhập các thông tin khác hợp lệ.<br>2. Nhập Họ tên: Chuỗi ngẫu nhiên 255 ký tự.<br>3. Nhấn nút "Cập nhật". | Hệ thống vẫn lưu thông tin, nhưng tên của User sau khi cập nhật có thể được cắt xén đi và không được phép làm vỡ layout. | Hệ thống lưu và cập nhật thông tin, tên User giữ nguyên 255 ký tự, làm vỡ layout, làm khuất đi 1 phần Lịch sử đơn hàng.  | Fail |
| **TC_FR20_06** | Báo lỗi khi số điện thoại không bắt đầu bằng số 0 | Người dùng đã đăng nhập thành công và đang ở màn hình Quản lý hồ sơ cá nhân. | 1. Nhập SĐT: `8912345678` (10 chữ số nhưng bắt đầu bằng số 8).<br>2. Nhấn nút "Cập nhật". | Hệ thống chặn lại, hiển thị thông báo lỗi: "Số điện thoại phải bắt đầu bằng số 0". Dữ liệu không được lưu. | Hệ thống thông báo: "Cập nhật thành công!", thông tin được lưu vào trong hệ thống. | Fail |
| **TC_FR20_07** | Xác nhận loại bàn phím hiển thị khi chọn ô nhập Số điện thoại (UI/UX) | Ứng dụng di động được chạy trên môi trường Expo/React Native. Người dùng đã đăng nhập. | 1. Chạm vào ô nhập dữ liệu của trường "Số điện thoại". | Bàn phím hệ thống tự động bật lên phải là bàn phím số (Numeric Keyboard), không hiển thị chữ cái. | Bàn phím hệ thống tự động bật lên khi ấn vào là bàn phím số, không hiển thị chữ cái. | Pass |
| **TC_FR20_08** | Xác nhận trường Email ở trạng thái không thể chỉnh sửa | Người dùng đã đăng nhập thành công và đang ở màn hình Quản lý hồ sơ cá nhân. | 1. Quan sát trường Email hiển thị thông tin.<br>2. Cố gắng chạm vào trường Email để kích hoạt con trỏ nhập liệu hoặc chỉnh sửa. | Trường Email hiển thị đúng địa chỉ của tài khoản nhưng ở trạng thái Read-only (vô hiệu hóa chỉnh sửa), không xuất hiện bàn phím. | Không thể chỉnh sửa trường Email dù cho click hay chạm vào trường Email. | Pass |
| **TC_FR20_09** | Kiểm tra dữ liệu Địa chỉ giao hàng mặc định được lưu sau khi đăng xuất và đăng nhập lại | Người dùng đã đăng nhập thành công, đã nhập Địa chỉ giao hàng mặc định hợp lệ và đang ở màn hình Quản lý hồ sơ cá nhân. | 1. Nhập hoặc cập nhật Địa chỉ giao hàng mặc định với một giá trị hợp lệ.<br>2. Nhấn nút "Cập nhật" và xác nhận hệ thống đã hiển thị thông báo cập nhật thành công.<br>3. Đăng xuất khỏi tài khoản.<br>4. Đăng nhập lại bằng đúng tài khoản vừa cập nhật.<br>5. Mở lại màn hình Quản lý hồ sơ cá nhân và kiểm tra trường Địa chỉ giao hàng mặc định. | Địa chỉ giao hàng mặc định phải được lưu lại đúng giá trị đã nhập trước đó và hiển thị lại sau khi đăng xuất/đăng nhập lại. | Sau khi cập nhật thành công, đăng xuất và đăng nhập lại, trường Địa chỉ giao hàng mặc định bị trống dù trước đó đã nhập dữ liệu. | Fail |

### 4. AI Gap Analysis
AI đã nhận diện đúng các phần cốt lõi của FR-20 như quyền sở hữu hồ sơ, SĐT bắt đầu bằng `0`, độ dài `10-11` chữ số và Email ở trạng thái read-only. Tuy nhiên vẫn còn các thiếu sót sau:

1. AI đề xuất kịch bản IDOR/cập nhật chéo tài khoản, nhưng kịch bản này không phù hợp với hệ thống thật vì backend xác thực bằng JWT, không tin vào định danh do client truyền lên. Vì vậy test case bảo mật đó không khả thi trên môi trường hiện tại.
2. AI chưa bao phủ tốt các hành vi đặc thù của mobile/UI thực tế như layout bị vỡ khi nhập Họ tên rất dài và việc dữ liệu Địa chỉ giao hàng mặc định phải được lưu lại sau khi đăng xuất/đăng nhập lại.
3. AI chưa đồng nhất hoàn toàn với giao diện thực tế của app, ví dụ tên nút và cách hiển thị trạng thái có thể đúng về mặt ý tưởng nhưng chưa khớp đầy đủ với flow mobile đang dùng.

Nguyên nhân chính của các thiếu sót này là AI ưu tiên suy luận từ mô tả nghiệp vụ và biên độ dữ liệu, trong khi FR-20 lại phụ thuộc thêm vào hành vi của ứng dụng mobile, trạng thái lưu trữ sau đăng nhập và chi tiết kiến trúc xác thực. Bản tinh chỉnh FR-20 đã khắc phục bằng cách bổ sung case kiểm tra layout với Họ tên 255 ký tự, case kiểm tra lưu Địa chỉ giao hàng mặc định sau khi đăng xuất/đăng nhập lại, đồng thời giữ lại các case BVA quan trọng cho SĐT và loại bỏ phần IDOR không khả thi.

### 5. Bug Report
Toàn bộ các bug phát hiện đã được báo cáo chi tiết, bao gồm ảnh chụp minh chứng, mô tả và link dẫn tới Github Issues ở file Bug_Report. 