+++
title = "Tạo S3 Bucket và CloudFront"
date = 2024
weight = 1
chapter = false
pre = "<b>2.1. </b>"
+++

## NỘI DUNG
Ở bước này bao gồm tạo **S3 Bucket** và **CloudFront** distribution để có thể truy cập và sử dụng nội dung.
- [NỘI DUNG](#nội-dung)
    - [Tạo S3 Bucket](#tạo-s3-bucket)
    - [Tải lên và xem ảnh/tệp tin/thư mục](#tải-lên-và-xem-ảnhtệp-tinthư-mục)
    - [Tạo CloudFront](#tạo-cloudfront)


#### Tạo S3 Bucket

1. Trên thanh tìm kiếm, tìm kiếm S3 và nhấn chọn để vào màn hình console của dịch vụ S3 Bucket.
![Image](../../../images/S3_Related/Console_1.jpg)
2. Nhấn vào **Create bucket** để tạo S3 Bucket mới.
3. Ở trang tạo S2 Bucket, điền tên Bucket muốn tạo và chọn ACLs disabled ở phần Object Ownership
![Image](../../../images/S3_Related/Name_ownership.jpg)

{{% notice note %}}
Tùy chọn ACLs (Access control list) disabled để cấu hình quyền sở hữu của tất cả các tệp, thư mục,... trong S3 Bucket đều là của tài khoản AWS này. Tất cả truy cập, chỉnh sửa đối với các object bên trong đều được quy định nhờ các **Policy** (IAM Policies and Permissions). Điều này làm tăng tính cá nhân, bảo mật, an toàn cho dữ liệu.
{{% /notice %}}

4. Các mục **Public Access** và **Bucket Versioning** để cấu hình mặc định.
![Image](../../../images/S3_Related/Access_version.jpg)

{{% notice note %}}
Chặn các truy cập public đảm bảo bảo mật, chỉ tương tác thông qua **CloudFront**, **API** (có xác thực).
{{% /notice %}}

5. Các mục **Tags**, **Default encryption (Mã hóa)** và **Advanced settings** để cấu hình mặc định
![Image](../../../images/S3_Related/Encrytion_setting.jpg)
![Image](../../../images/S3_Related/Advanced_setting.jpg)

6. Nhấn **Create bucket**, S3 Bucket của bạn đã được tạo thành công.
![Image](../../../images/S3_Related/Console_2.jpg)

#### Tải lên và xem ảnh/tệp tin/thư mục
1. Nhấn chọn nút **Upload**
![Image](../../../images/S3_Related/Upload_console_1.jpg)
2. Chọn **Add files/Add folder** tương ứng loại object mà bạn muốn tải lên và nhấn **Upload**
![Image](../../../images/S3_Related/Upload_console_2.jpg)
Upload thành công
![Image](../../../images/S3_Related/Upload_console_3.jpg)
![Image](../../../images/S3_Related/Upload_console_4.jpg)
3. Có thể xem nội dung (đối với ảnh), hoặc tải về bằng nút **Open**.
![Image](../../../images/S3_Related/Upload_console_5.jpg)

{{% notice note %}}
Có thể xem/tải xuống bằng URL ở Object URL nếu bỏ tùy chọn Block Public Access tương ứng (Ở mục tạo Bucket).
{{% /notice %}}

#### Tạo CloudFront
1. Trên thanh tìm kiếm, tìm kiếm CloudFront và nhấn chọn để vào giao diện của dịch vụ AWS CloudFront. Nhấn **Create distribution** để tạo Distribution mới.
![Image](../../../images/CloudFront_Related/Console_1.jpg)
2. Chọn Origin domain là domain của S3 Bucket đã tạo ở trên. Chọn OAC (Origin Access Control) tới S3 Bucket đã tạo.
![Image](../../../images/CloudFront_Related/Console_2.jpg)
*Nếu OAC chưa tồn tại thì nhấn Create new OAC để tạo mới.*
![Image](../../../images/CloudFront_Related/OAC_Create.jpg)
4. Các mục sau làm theo các bước dưới đây.
![Image](../../../images/CloudFront_Related/Console_3.jpg)
![Image](../../../images/CloudFront_Related/Console_4.jpg)
5. Nhấn **Create distribution** để khởi tạo.
6. Ở màn hình sau khởi tạo sẽ có hiện một cảnh, yêu cầu thêm policy để cấp quyền cho **CloudFront** có thể truy cập vào nội dung lưu trữ trong S3 Bucket. Nhấn Copy policy và quay lại giao diện quản lý của S3 Bucket.
![Image](../../../images/CloudFront_Related/Console_5.jpg)
7. Chọn vào S3 Bucket đã tạo, nhấn vào tab Permissions và kéo xuống phần Bucket policy sau đó nhấn **Edit**.
![Image](../../../images/CloudFront_Related/S3_Policy.jpg)
8. Dán Policy đã sao chép sau đó nhấn **Save changes**.
![Image](../../../images/CloudFront_Related/S3_Policy_2.jpg)
7. Quay lại chi tiết của Distribution CloudFront vừa tạo xong (Hiển thị thời gian ở mục **Last modified**). Sao chép **Distribution domain name** của distribution (Dùng để truy cập các nội dung trên Origin domain).
![Image](../../../images/CloudFront_Related/Console_6.jpg)
8. Truy cập xem/tải nội dung trong S3 Bucket bằng cách nhập url + đường dẫn tới tệp lưu trữ trên S3 (Trong thư mục con thì thêm '/').
![Image](../../../images/CloudFront_Related/Image_Show.jpg)

Vậy là hoàn thành xong bước đầu tiên, tạo S3 Bucket và CloudFront để xem/sử dụng nội dung trong kho lưu trữ.

