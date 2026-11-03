**1\. Bối cảnh**

Nam là thực tập sinh tại GreenLogistics. Nam nhận nhiệm vụ truy cập trang quản trị tại địa chỉ [**phong-dieu-phoi.greenlog.vn**](http://phong-dieu-phoi.greenlog.vn) để cập nhật lộ trình xe tải. Tuy nhiên, trình duyệt liên tục báo lỗi **"DNS\_PROBE\_FINISHED\_NXDOMAIN"**. Nam khẳng định do máy chủ công ty bị sập nguồn.

**2\. Yêu cầu**

* **Chức năng 1 (Phân tích mạng):** Giải thích chi tiết tiến trình DNS Lookup từ khi Nam gõ tên miền đến khi trình duyệt tìm thấy địa chỉ IP máy chủ.  
* **Chức năng 2 (Chẩn đoán lỗi):** Phân biệt bản chất giữa lỗi DNS và lỗi 500 Internal Server Error để xác định lỗi này nằm ở phía Client hay Server.

**3\. Ràng buộc**

Nam đang gõ nhầm địa chỉ thành [**phong-dieu-phoi.grenlog.vn**](http://phong-dieu-phoi.grenlog.vn) (thiếu một chữ 'e'). Hãy chỉ ra hậu quả của việc sai lệch tên miền trong "cuốn danh bạ Internet".

**4\. Yêu cầu đầu ra**

***Phần 1\. Phân tích***

* Xác định Input (Tên miền) / Output (IP address) và mô tả sơ đồ luồng dữ liệu của DNS.  
- Input : Tên miền do người dùng nhập vào trình duyệt (phong-dieu-phoi.grenlog.vn).  
- Output : Địa chỉ IP của máy chủ tương ứng 

***Phần 2\. Triển khai***

* Đề xuất quy trình kiểm tra mã trạng thái HTTP Status Code để xác nhận xem yêu cầu đã chạm tới máy chủ hay chưa.  
- Browser Cache: Trình duyệt kiểm tra xem đã lưu IP của tên miền này gần đây hay chưa.  
- OS Cache : Trình duyệt hỏi hệ điều hành xem có lưu bản ghi DNS hoặc cấu hình trong file hosts hay không.  
- Recursive Resolver : Nếu OS không có, hệ điều hành gửi yêu cầu đến Máy chủ phân giải đệ quy   
- Root Name Server: Nếu Resolver chưa biết, nó hỏi máy chủ gốc quản lý toàn cầu. Root Server sẽ điều hướng về máy chủ quản lý đuôi .vn.  
- TLD Name Server : Máy chủ tên miền cấp cao nhất của .vn sẽ chỉ dẫn đến Máy chủ ủy quyền của công ty grenlog.vn.  
- Authoritative Name Server : Máy chủ chứa dữ liệu chính thức của tên miền kiểm tra xem có bản ghi cho phong-dieu-phoi.grenlog.vn hay không.

***Phần 3\. Kiểm thử***

* Giả định Nam sửa đúng tên miền nhưng vẫn nhận mã **404 Not Found**, hệ thống đang gặp vấn đề gì?  
- Không tìm thấy dữ liệu, trang không tồn tại 

