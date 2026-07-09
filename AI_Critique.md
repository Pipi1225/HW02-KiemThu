# AI CRITIQUE

- Student name: Dương Gia Huy
- Student ID: 23127052

---

AI có khả năng khởi tạo test case nhanh và đúng hướng, đặc biệt khi áp dụng Domain Testing và BVA, nhưng qua cả 4 artifact thì kết quả vẫn chỉ ở mức INCOMPLETE vì chưa bám sát đầy đủ hành vi thực tế của hệ thống và còn đôi khi đưa ra các kịch bản không khả thi với kiến trúc triển khai. 
<br>Tuy AI thể hiện tốt việc tạo lập bộ khung kiểm thử cơ bản, nhưng kết quả đầu ra thường không hoàn chỉnh và thiếu tính thực tiễn. Cụ thể, AI đã sai khi đề xuất kịch bản bảo mật IDOR không khả thi, do không hiểu rằng backend thực tế xác thực người dùng qua JWT thay vì định danh từ client gửi lên. AI cũng mắc thiên kiến bám sát văn bản, dẫn đến việc bỏ sót các thành phần giao diện có thật trong source code nhưng không nằm trong đặc tả (như trường "URL ảnh" hay nút "Mua tiếp"). 
<br>Nguyên nhân của những thiếu sót này là do AI chỉ xử lý logic trên bề mặt ngôn ngữ, nó không thể tự thực hiện kiểm thử khám phá hay dự đoán các lỗi liên quan đến trạng thái ứng dụng như mất dữ liệu giỏ hàng khi F5, lỗi nhập số âm từ trang chi tiết hay lỗi vỡ layout trên màn hình Mobile. 
<br>Từ đó, nguyên tắc cốt lõi em rút ra là: AI chỉ nên đóng vai trò trợ lý cung cấp nền tảng ban đầu. Sự can thiệp và đánh giá của con người là bắt buộc để tinh chỉnh kịch bản khớp với kiến trúc thực tế và đảm bảo trải nghiệm người dùng toàn diện.