+++
title = "Thử API bằng Postman"
date = 2024
weight = 3
chapter = false
pre = "<b>3. </b>"
+++

## Nội dung

Ở bước cuối cùng này, chúng ta sẽ cùng thử các API Upload và Delete vừa tạo bằng ứng dụng Postman.

#### Thử API Upload (PUT)

1. Chọn phương thức PUT, nhập đường dẫn API Upload (xem ở phần **Stages**). Trong body chọn file muốn tải lên sau đó nhấn **Send**.
   ![Image](../images/API%20Gateway/Postman_test_1.jpg)
   Như chúng ta thấy kết quả sẽ trả về Forbidden 403 vì chúng ta chưa thêm API key cho xác thực
   ![Image](../images/API%20Gateway/Postman_test_2.jpg)
2. Giờ thêm API key trong mục **Authorization** và nhấn **Send** lần nữa.
   ![Image](../images/API%20Gateway/Postman_success_1.jpg)
   Giờ thì kết quả trả về giống với định dạng chúng ta làm trong phần **Integration response**, bao gồm status và url CloudFront của file vừa được upload.
3. Nhấn vào url để xem ảnh.
   ![Image](../images/API%20Gateway/Postman_success_2.jpg)
4. Vào S3 và chúng ta sẽ thấy ảnh vừa được upload.
   ![Image](../images/API%20Gateway/Postman_success_3.jpg)

#### Thử API Delete (DELETE)

1. Chọn phương thức DELETE, nhập đường dẫn API DELETE (xem ở phần **Stages**). Trong body chọn file muốn tải lên sau đó nhấn **Send**.
   ![Image](../images/Lambda/Deploy_3.jpg)
   Kết quả trả về là message thông báo đã xóa thành công.
2. Vào S3 và chúng ta sẽ thấy file đã được xóa.
   ![Image](../images/Lambda/Deploy_4.jpg)

Chúng ta đã hoàn thành việc tạo một kho lưu trữ ảnh đơn giản.
