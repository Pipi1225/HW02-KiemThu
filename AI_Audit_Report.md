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

**4. Reasoning:** Các test case do AI tạo đã bao phủ hầu hết các domain cần kiểm tra (happy path các edge cases và cả về bảo mật tài khoản), nhưng vẫn còn thiếu test case kiểm tra ràng buộc về loại ký tự của biến số điện thoại (như `098abc1041` hoặc `098-102-512`) để hoàn toàn đạt được coverage 100%.

**5. Student Fix:** Bổ sung thêm test case TC_FR04_06: kiểm tra lỗi SĐT chứa ký tự chữ cái hoặc ký tự đặc biệt để bao phủ toàn bộ.

### Artifact 2: 
**1. Prompt + Tool**
- **Tool:** 
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