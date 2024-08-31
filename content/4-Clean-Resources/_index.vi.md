+++
title = "Dọn dẹp tài nguyên"
date = 2024
weight = 4
chapter = false
pre = "<b>4. </b>"
+++

## Nội dung

Sau khi hoàn thành, nếu không sử dụng chúng ta sẽ tiến hành dọn dẹp các tài nguyên đã tạo trong bài để tránh việc mất phí.

#### Xóa S3 Bucket

1. Đầu tiên phải làm trống S3 Bucket muốn xóa, có thể dùng nút **Empty** ở bên ngoài thay vì xóa từng files.
   ![Image](../images/Clean%20Resources/S3_00.jpg)
2. Tiếp theo chọn **Delete** và xác nhận xóa.
   ![Image](../images/Clean%20Resources/S3_03.jpg)

#### Xóa Lambda function

![Image](../images/Clean%20Resources/Lambda_1.jpg)

#### Xóa CloudFront

1. Trước khi xóa phải disable distribution muốn xóa. (Quá trình này có thể mất vài phút)
   ![Image](../images/Clean%20Resources/CF_1.jpg)
   ![Image](../images/Clean%20Resources/CF_3.jpg)
2. Xóa distribution bằng nút **Delete**.
   ![Image](../images/Clean%20Resources/CF_4.jpg)

#### Xóa API Gateway

1. Delete Stages.
   ![Image](../images/Clean%20Resources/APIGW_1.jpg)
2. Delete API.
   ![Image](../images/Clean%20Resources/APIGW_2.jpg)
