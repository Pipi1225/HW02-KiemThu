# BUG REPORT

- Student name: Dương Gia Huy
- Student ID: 23127052

---

## Feature 1: FR-04: Quản lý hồ sơ cá nhân

### Bug 1: Sai logic xác thực độ dài số điện thoại khi cập nhật hồ sơ (Đặc tả nhận 10-11 số, thực tế chỉ nhận 9-10 số)
- **Mô tả Bug:**
Theo đặc tả hệ thống (FR-04), số điện thoại hợp lệ phải có độ dài từ 10 đến 11 chữ số. Tuy nhiên, hiện tại hệ thống chỉ chấp nhận SĐT từ 9 đến 10 chữ số và hiển thị thông báo lỗi không chính xác từ đó dẫn đến việc người dùng không thể cập nhật SĐT hợp lệ có 11 số, và SĐT 10 số cũng bị bắt lỗi một cách bất thường.

- **Test Case liên quan:**
    - `TC_FR04_01`
    - `TC_FR04_02`
    - `TC_FR04_03`
    - `TC_FR04_04`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/46
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 1](images/TC_FR04_1_1.jpg)

### Bug 2: Hệ thống chấp nhận lưu số điện thoại không bắt đầu bằng số 0
- **Mô tả Bug:**
Theo đặc tả hệ thống (FR-04), số điện thoại hợp lệ phải bắt đầu với số 0. Tuy nhiên, hiện tại hệ thống đang thiếu logic xác thực hoặc thậm chí là sai logic xác thực như đã báo cáo trong `Bug 1`, các số điện thoại bắt đầu bằng số 0 hệ thống đều không chấp nhận. Ngược lại người dùng có thể nhập các số điện thoại bắt đầu bằng chữ số khác (Ví dụ: 8, 9...) và hệ thống vẫn chấp nhận, báo thành công và lưu trực tiếp vào cơ sở dữ liệu.

- **Test Case liên quan:**
    - `TC_FR04_05`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/47
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 2](images/TC_FR04_2_1.jpg)

### Bug 3: Hiển thị chung một thông báo lỗi sai ngữ cảnh cho mọi thao tác nhập liệu không hợp lệ tại trường số điện thoại
- **Mô tả Bug:**
Hệ thống hiện đang sử dụng một thông báo lỗi dùng chung cho mọi trường hợp nhập liệu không hợp lệ tại trường "Số điện thoại". Bất kể người dùng bỏ trống, nhập chữ cái/ký tự đặc biệt, hay nhập sai đầu số, hệ thống đều trả về duy nhất một câu thông báo: "Số điện thoại không hợp lệ. Vui lòng nhập đúng 9-10 chữ số" (sai lệch so với đặc tả - giới hạn độ dài chỉ từ 10 - 11 số).

- **Test Case liên quan:**
    - `TC_FR04_01`
    - `TC_FR04_02`
    - `TC_FR04_03`
    - `TC_FR04_04`
    - `TC_FR04_06`
    - `TC_FR04_07`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/48
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 3](images/TC_FR04_3_1.jpg)
![Screenshot 2 - Bug 3](images/TC_FR04_3_2.jpg)

### Bug 4: Người dùng có thể tự nâng quyền thành Admin qua API cập nhật hồ sơ (Mass Assignment)
- **Mô tả Bug:**
Hệ thống đang mắc phải lỗ hổng bảo mật nghiêm trọng Mass Assignment, khi người dùng gọi API cập nhật hồ sơ cá nhân và cố tình chèn thêm thuộc tính phân quyền (`"role": "admin"`) vào payload request, Backend đã không thực hiện kiểm soát và lọc dữ liệu đầu vào mà trực tiếp lưu toàn bộ payload nhận được vào cơ sở dữ liệu, dẫn đến việc một tài khoản thông thường (user) có thể tự nâng đặc quyền của mình lên quản trị viên (admin) trái phép.

- **Test Case liên quan:**
    - `TC_FR04_09`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/49
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 4](images/TC_FR04_4_1.jpg)
![Screenshot 2 - Bug 4](images/TC_FR04_4_2.jpg)

### Bug 5: Thiếu hình minh họa khi giao diện Giỏ hàng ở trạng thái trống
- **Mô tả Bug:**
Theo đặc tả hệ thống (FR-07), khi người dùng truy cập vào giỏ hàng nhưng chưa có sản phẩm nào, hệ thống bắt buộc phải hiển thị kết hợp cả thông báo bằng chữ và hình ảnh minh họa trạng thái trống. Tuy nhiên, hiện tại giao diện chỉ hiển thị duy nhất dòng chữ "Giỏ hàng của bạn đang trống", hoàn toàn thiếu đi hình ảnh minh hoạ.

- **Test Case liên quan:**
    - `TC_FR07_01`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/54
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 5](images/TC_FR07_1_1.jpg)

### Bug 6: Giao diện giỏ hàng thiếu nút tăng/giảm (+/-) tại cột Số lượng sản phẩm trong Giỏ hàng
- **Mô tả Bug:**
Theo đặc tả hệ thống (FR-07), cột "Số lượng" trong danh sách sản phẩm bắt buộc phải có kèm theo nút + và - để người dùng có thể điều chỉnh số lượng mua trực tiếp. Tuy nhiên, trên giao diện thực tế hiện tại, cột "Số lượng" hoàn toàn khuyết thiếu hai nút thao tác này (vấn đề tương tự bên giao diện giỏ hàng mobile ở github issues #50 có đề cập). Điều này làm phá vỡ trải nghiệm mua sắm vì người dùng không thể cập nhật số lượng ngay tại giỏ hàng.
(Lưu ý: Tên cột tiêu đề Đơn giá hiện đang bị render sai thành Giá).

- **Test Case liên quan:**
    - `TC_FR07_02`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/55
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 6](images/TC_FR07_2_1.jpg)

### Bug 7: Hiển thị sai nhãn tổng tiền trong Giỏ hàng ("Tổng tạm tính" thay vì "Tổng cộng")
- **Mô tả Bug:**
Đặc tả hệ thống (FR-07) quy định rất rõ ràng và nhấn mạnh việc nhãn hiển thị tổng tiền trong Giỏ hàng phải là "Tổng cộng" (tuyệt đối không dùng "Tổng tạm tính"). Tuy nhiên, trên giao diện hiện tại, mặc dù hệ thống tính toán ra số tiền chính xác, nhưng nhãn text lại đang bị hardcode sai thành "Tổng tạm tính".

- **Test Case liên quan:**
    - `TC_FR07_03`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/56
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 7](images/TC_FR07_3_1.jpg)

### Bug 8: Hệ thống sinh dòng mới thay vì cộng dồn số lượng khi thêm sản phẩm trùng lặp vào Giỏ hàng
- **Mô tả Bug:**
Theo đặc tả hệ thống (FR-07), khi người dùng thêm cùng một sản phẩm đã tồn tại trong giỏ hàng, hệ thống phải cập nhật tăng số lượng của dòng sản phẩm đó lên, tuyệt đối không tạo thêm dòng mới. Tuy nhiên, logic xử lý thêm vào giỏ hàng (addToCart) hiện tại đang bị sai: mỗi lần nhấn "Thêm vào giỏ" đối với một sản phẩm trùng lặp, hệ thống lại sinh ra một dòng dữ liệu hoàn toàn riêng biệt trong danh sách giỏ hàng.

- **Test Case liên quan:**
    - `TC_FR07_04`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/57
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 8](images/TC_FR07_4_1.jpg)

### Bug 9: Xóa sản phẩm ngay lập tức mà không hiển thị Dialog xác nhận
- **Mô tả Bug:**
Theo đặc tả hệ thống (FR-07), thao tác "Xóa sản phẩm" khỏi Giỏ hàng bắt buộc phải hiển thị một Dialog xác nhận (Confirmation Dialog) để ngăn chặn việc người dùng click nhầm. Tuy nhiên, hiện tại hệ thống đang thực thi lệnh xóa ngay lập tức (instant delete) ngay khi người dùng nhấn vào nút Xóa ở cột Thao tác. Không có bất kỳ cảnh báo hay hộp thoại nào được hiển thị, gây rủi ro mất dữ liệu giỏ hàng do vô tình thao tác sai.

- **Test Case liên quan:**
    - `TC_FR07_08`
    - `TC_FR07_09`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/58
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 9](images/TC_FR07_5_1.jpg)
![Screenshot 2 - Bug 9](images/TC_FR07_5_2.jpg)

### Bug 10: Mất toàn bộ dữ liệu giỏ hàng khi làm mới (Refresh/F5) trang
- **Mô tả Bug:**
Hệ thống hiện không có cơ chế lưu trữ bền vững (State Persistence) cho dữ liệu Giỏ hàng. Khi người dùng đang có sản phẩm trong giỏ và thực hiện thao tác tải lại trang (Refresh/F5), toàn bộ dữ liệu bị xóa sạch, giỏ hàng quay về trạng thái trống trơn ban đầu. Điều này vi phạm nghiêm trọng luồng trải nghiệm mua sắm cơ bản, gây ức chế và rủi ro mất khách hàng.

- **Test Case liên quan:**
    - `TC_FR07_12`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/59
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 10](images/TC_FR07_6_1.jpg)
![Screenshot 2 - Bug 10](images/TC_FR07_6_2.jpg)

### Bug 11: Cho phép nhập số lượng sản phẩm là số âm vào Giỏ hàng
- **Mô tả Bug:**
Hệ thống hiện đang thiếu hoàn toàn cơ chế xác thực dữ liệu đối với trường Số lượng sản phẩm. Người dùng có thể cố tình nhập một số âm (Ví dụ: `-5`) khi thêm sản phẩm từ trang chi tiết Sản phẩm và hệ thống vẫn chấp nhận đưa sản phẩm đó vào Giỏ hàng.

- **Test Case liên quan:**
    - `TC_FR07_13`

- **Github Issues Link:** https://github.com/nguyenhieuthuan3105/EShop-Testing-HW02-Group04/issues/61
- **Ảnh minh chứng (Screenshots):**
![Screenshot 1 - Bug 11](images/TC_FR07_7_1.jpg)

### Bug 12: 
- **Mô tả Bug:**

- **Test Case liên quan:**
    - ``

- **Github Issues Link:** 
- **Ảnh minh chứng (Screenshots):**

### Bug 13: 
- **Mô tả Bug:**

- **Test Case liên quan:**
    - ``

- **Github Issues Link:** 
- **Ảnh minh chứng (Screenshots):**

### Bug 14: 
- **Mô tả Bug:**

- **Test Case liên quan:**
    - ``

- **Github Issues Link:** 
- **Ảnh minh chứng (Screenshots):**

### Bug 15: 
- **Mô tả Bug:**

- **Test Case liên quan:**
    - ``

- **Github Issues Link:** 
- **Ảnh minh chứng (Screenshots):**

### Bug 16: 
- **Mô tả Bug:**

- **Test Case liên quan:**
    - ``

- **Github Issues Link:** 
- **Ảnh minh chứng (Screenshots):**

### Bug 17: 
- **Mô tả Bug:**

- **Test Case liên quan:**
    - ``

- **Github Issues Link:** 
- **Ảnh minh chứng (Screenshots):**