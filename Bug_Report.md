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

### Bug 5: 
- **Mô tả Bug:**

- **Test Case liên quan:**
    - ``

- **Github Issues Link:** 
- **Ảnh minh chứng (Screenshots):**

### Bug 6: 
- **Mô tả Bug:**

- **Test Case liên quan:**
    - ``

- **Github Issues Link:** 
- **Ảnh minh chứng (Screenshots):**