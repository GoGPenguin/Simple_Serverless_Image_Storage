+++
title = "Tạo API Gateway"
date = 2024
weight = 3
chapter = false
pre = "<b>2.3. </b>"
+++

## Nội dung

Ở bước này chúng ta sẽ tạo API Gateway. Cụ thể là 1 API sử dụng S3 Integration để upload tệp lên S3 bucket, API còn lại để kích hoạt Lambda function tạo ở bước trước đó để xóa tệp chỉ định trong S3 bucket.

#### Tạo Upload API (PUT)

1. Trên thanh tìm kiếm, tìm API Gateway và nhấn chọn để vào trang của dịch vụ AWS API Gateway. Nhấn **Create API**, chọn **REST API** sau đó nhấn **Build**.
   ![Image](../../images/API%20Gateway/Console_1.jpg)
2. Điền tên API, các tùy chọn còn lại để mặc định sau đó nhấn **Create API**.
   ![Image](../../images/API%20Gateway/Console_2.jpg)
3. Tự động điều hướng sang trang quản lý API vừa tạo. Chọn '/' sau đó nhấn **Create resource**.
   ![Image](../../images/API%20Gateway/Console_3.jpg)
4. Tương tự làm theo các bước như hình sau:
   ![Image](../../images/API%20Gateway/Console_4.jpg)
   ![Image](../../images/API%20Gateway/Console_5.jpg)
   ![Image](../../images/API%20Gateway/Console_6.jpg)
5. Nhấn vào '**/{key}**' và chọn **Create method**.
   ![Image](../../images/API%20Gateway/Console_7.jpg)
6. Với Upload file thì ở **Method type** chọn **PUT**, chọn **Region** tương ứng, để tương tác với S3 chúng ta chọn AWS Service là **Simple Storage Service (S3)**. **HTTP Method** chọn **PUT**.
   ![Image](../../images/API%20Gateway/Create_method_1.jpg)
7. Các bước sau làm theo hình. Ở **Excution role**, tạo 1 Role tương tự như cách tạo IAM Role cho Lambda nhưng AWS Service là API Gateway, với các policy tương ứng. Sau đó dán arn của IAM Role vào cho method.
   ![Image](../../images/API%20Gateway/Create_method_2.jpg)
8. Chọn API key required ở phần mở rộng **Method request settings** sau đó nhấn **Create method**.
   ![Image](../../images/API%20Gateway/Create_method_3.jpg)
9. Method được tạo thành công. Nhấn vào tab **Integration request** sau đó chọn **Edit**.
   ![Image](../../images/API%20Gateway/Create_method_4.jpg)
10. Ở phần mở rộng URL path parameters, **Add path parameter** như hình . Sau đó nhấn **Save changes**.
    `Name: bucket, Mapped from: method.request.path.bucket (tương ứng các parameters trên đường dẫn).`
    `Name: filekey, Mapped from: method.request.path.key (tương ứng các parameters trên đường dẫn).`
    ![Image](../../images/API%20Gateway/Create_method_5.jpg)
11. Chọn **API settings** ở thanh bên, sau đó nhấn **Manage media types** để thêm các loại dữ liệu binary API có thể nhận.
    ![Image](../../images/API%20Gateway/API_Setting_1.jpg)
12. Thêm các **Binary media type** sau để tương tác với các file dạng ảnh sau đó lưu lại.
    ![Image](../../images/API%20Gateway/API_Setting_2.jpg)
13. Ở tab **Integration response** của PUT method vừa tạo, chọn **Edit**.
    ![Image](../../images/API%20Gateway/API_Setting_3.jpg)
14. Ở phần mở rộng **Mapping templates**, có thể tùy chỉnh phản hồi của API. Ở đây, mình cấu hình API sẽ trả về đường dẫn CloudFront của file nếu upload thành công. Sau đó lưu lại.
    ![Image](../../images/API%20Gateway/API_Setting_4.jpg)
15. Quay lại trang của PUT method vừa tạo, chọn **Deploy API**.
16. Chọn hoặc tạo mới Stage sau đó nhấn **Deploy**.
    {{% notice note %}}
    Stage là các snapshot cho API. Ví dụ như api v1, api v2,...
    {{% /notice %}}
    ![Image](../../images/API%20Gateway/Deploy_API_1.jpg)
17. Sau khi deploy thành công, chọn **Stages** bên thanh chức năng, nhấn vào API tương ứng để có thể xem đường dẫn gọi API
    ![Image](../../images/API%20Gateway/Deploy_API_2.jpg)
    Tiếp theo là các bước tạo API Key và Usage plan cho API.
    {{% notice note %}}
    **API key** dùng để xác thực khi gọi API, tránh trường hợp API được gọi cho các mục đích xấu, sử dụng bởi những người không có quyền sở hữu.  
    **Usage plan** sử dụng để hạn chế các hành vi như spam gọi API, quy định số yêu cầu đồng thời tới API...
    {{% /notice %}}
18. Ở thanh chức năng, chọn API keys sau đó nhấn **Create API key**.
19. Điền tên API key rồi lưu lại.
    ![Image](../../images/API%20Gateway/APIKey.jpg)
20. Sao chép API key vừa tạo.
    ![Image](../../images/API%20Gateway/APIKey_2.jpg)
21. Ở phần **Usage plan**, nhấn **Create usage plan**.
22. Điền các cấu hình mong muốn. **Rate**: Số request mỗi giây. **Burst**: Số request đồng thời. **Requests**: Số requests người dùng có thể yêu cầu trong một khoảng thời gian (mỗi ngày, mỗi tháng,...). Sau đó nhấn **Create usage plan**.
    ![Image](../../images/API%20Gateway/APIKey_3.jpg)
23. Quay lại **APIs key**, chọn API key vừa tạo sau đó nhấn **Add to usage plan** để gán API với Usage plan mong muốn.
    ![Image](../../images/API%20Gateway/APIKey_4.jpg)
24. Ở tab **Associated stages**, chọn **Add stage** để thêm API đã Deploy có thể sử dụng Usage plan.
    ![Image](../../images/API%20Gateway/APIKey_5.jpg)
    ![Image](../../images/API%20Gateway/APIKey_6.jpg)

#### Tạo Delete API (DELETE)

1. Ở mục **Resources** bên thanh chức năng, chọn Create method.
2. Chọn **Method type** là **DELETE**. Vì API kích hoạt Lambda function chúng ta đã tạo trước đó nên thực hiện cấu hình như hình dưới.
   ![Image](../../images/Lambda/API_Lambda_1.jpg)
3. Sau đó nhấn **Create method**.
   ![Image](../../images/Lambda/API_Lambda_2.jpg)
4. Delete API đã được tạo thành công.
   ![Image](../../images/Lambda/API_Lambda_3.jpg)
5. Tương tự tiến hành Deploy Delete API.
   ![Image](../../images/Lambda/Deploy_1.jpg)
   ![Image](../../images/Lambda/Deploy_2.jpg)

Vậy là chúng ta đã tạo xong 2 API cho Upload và Delete. Giờ chúng ta sẽ tới bước thử nghiệm.
