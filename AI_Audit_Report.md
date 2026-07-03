# AI AUDIT REPORT

- Student name: Dương Gia Huy
- Student ID: 23127052

## AI-generated Artifact

### Artifact 1: 
**1. Prompt + Tool**
- **Tool:** Gemini 3.1 Pro
- **Timestamp:** 09:14 30/06/2026
- **Prompt:** Yêu cầu áp dụng kỹ thuật Phân tích Miền (Domain Testing) và Phân tích Giá trị biên (BVA) để thiết kế kịch bản kiểm thử (Test Cases) cho tính năng FR-04: Quản lý hồ sơ cá nhân với các ràng buộc cụ thể về dữ liệu, phân quyền và hiển thị.

**2. AI Output:** Đã tạo thành công 1 bảng phân tích Domain (8 thuộc tính), 1 bảng phân tích BVA (cho độ dài Số điện thoại) và 8 Test Cases chi tiết bao phủ Happy path (SĐT 10-11 số hợp lệ), Edge cases (sai định dạng, BVA Min-1/Max+1) cùng các kịch bản kiểm thử bảo mật (Email read-only, chặn đổi Role, chặn đổi profile người khác).

**3. Verdict:** INCOMPLETE

**4. Reasoning:** 
- Các test case do AI tạo đã bao phủ hầu hết các domain cần kiểm tra, bao gồm happy path các edge cases và cả về bảo mật tài khoản theo đặc tả nhưng vẫn chưa đạt được coverage 100%, do vẫn còn thiếu test case kiểm tra ràng buộc về loại ký tự của biến số điện thoại (như `098abc1041` hoặc `098-102-512`) và kiểm tra dữ liệu rỗng đối với trường SĐT
- AI đã đề xuất một kịch bản kiểm tra bảo mật (thay đổi user id trong request payload để cập nhật hồ sơ tài khoản khác) nhưng test case không khả thi đối với hệ thống hiện tại, do backend thực hiện xác thực user bằng cách giải mã trực tiếp từ token JWT gửi lên qua header.

**5. Student Fix:** Bổ sung thêm 2 test cases `TC_FR04_06: kiểm tra lỗi SĐT chứa ký tự chữ cái hoặc ký tự đặc biệt` và `TC_FR04_07: Báo lỗi khi bỏ trống SĐT` để bao phủ toàn bộ theo đặc tả và loại bỏ (bỏ qua) test case `TC_FR04_10: kiểm tra cập nhật chéo tài khoản` của AI do kiến trúc dùng JWT. Và tinh chỉnh lại phần test steps của `TC_FR04_09: Không thể tự ý thay đổi thuộc tính Role` để thực hiện dễ dàng hơn.

### Artifact 2: 
**1. Prompt + Tool**
- **Tool:** Gemini 3.1 Pro
- **Timestamp:** 16:08 01/07/2026
- **Prompt:** Yêu cầu thiết kế kịch bản kiểm thử cho tính năng Giỏ hàng (FR-07) bao gồm hiển thị danh sách, thêm/xóa/sửa số lượng sản phẩm, kiểm tra nhãn tổng tiền và trạng thái giỏ hàng trống dựa trên điều kiện context.

**2. AI Output:** Đã tạo 9 Test Cases bao phủ các luồng xử lý và giao diện bằng việc áp dụng kỹ thuật Phân tích Miền (Domain Testing) để kiểm tra các trạng thái hợp lệ/không hợp lệ và Phân tích Giá trị biên (BVA) cho biến số lượng (Min = 1).

**3. Verdict:** INCOMPLETE

**4. Reasoning:**
- Các test case do AI tạo đa phần chỉ tập trung vào giao diện (1 phần là do prompt ràng buộc AI chỉ chú ý tới đặc tả) mà bỏ sót các lỗi kinh điển trong thương mại điện tử (như mất dữ liệu khi refresh trang - F5, thêm vào giỏ hàng với số lượng sản phẩm là số âm từ trang chi tiết sản phẩm). Và thiếu 1 test case (`TC_FR07_11: Kiểm tra chức năng của nút "Mua tiếp"`) do nút "Mua tiếp" không hề được đề cập trong đặc tả nhưng lại có trong giao diện giỏ hàng.
- Bên cạnh đó còn có 1 test case mà AI vi phạm nguyên tắc kiểm thử độc lập (gộp chung thao tác tăng và giảm số lượng vào một kịch bản).

**5. Student Fix:** Em đã tách ra test case mà AI vi phạm (gộp chung thao tác tăng và giảm số lượng vào một kịch bản) thành 2 test cases riêng biệt `TC_FR07_05` và `TC_FR07_06`, đồng thời bổ sung thêm 3 test cases `TC_FR07_11: Kiểm tra chức năng của nút "Mua tiếp"`, `TC_FR07_12: Kiểm tra tính nhất quán trạng thái của giỏ hàng`, `TC_FR07_13: Giao diện và API cho phép người dùng nhập và lưu số lượng sản phẩm là số âm` để đảm bảo bao phủ đầy đủ và tinh chỉnh lại test steps cho các test cases cho chi tiết hơn.

### Artifact 3: 
**1. Prompt + Tool**
- **Tool:** Gemini 3.1 Pro
- **Timestamp:** 
- **Prompt:** 

**2. AI Output:** 

**3. Verdict:** 

**4. Reasoning:**

**5. Student Fix:**

### Artifact 4: 
**1. Prompt + Tool**
- **Tool:** Gemini 3.1 Pro
- **Timestamp:** 
- **Prompt:** 

**2. AI Output:** 

**3. Verdict:** 

**4. Reasoning:**

**5. Student Fix:**

### Artifact 5: 
**1. Prompt + Tool**
- **Tool:** Gemini 3.1 Pro
- **Timestamp:** 
- **Prompt:** 

**2. AI Output:** 

**3. Verdict:** 

**4. Reasoning:**

**5. Student Fix:**

## Đánh giá & Kết luận

### Đánh giá độ chính xác của AI
* **VALID: 0/0 (0%)** 
  *()*
* **INCOMPLETE: 0/0 (0%)** 
  *()*.
* **INVALID: 0/0 (0%)**
  *()*

### Kết luận
Thông qua quá trình thực hiện bài tập và đối chiếu kết quả, em rút ra kết luận về việc ứng dụng AI như sau:
**Khi nào nên dùng AI:**
1. 

**Khi nào không nên dùng AI:**
1. 