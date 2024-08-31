+++
title = "Tạo các tài nguyên cần thiết"
date = 2024
weight = 2
chapter = false
pre = "<b>2. </b>"
+++

Ở bước này, chúng ta sẽ khởi tạo các tài nguyên cần thiết.  
Đầu tiên, tạo S3 Bucket để lưu trữ hình ảnh và CloudFront để có thể sử dụng các hình ảnh đã được lưu trữ.  
Bước thứ hai là tạo Lambda với chức năng xóa tệp hình ảnh trong S3 (Serverless).
Ở bước thứ ba sẽ tạo API Gateway để có thể tương tác với S3 Bucket thông qua API và S3 Bucket Integration để làm chức năng upload ảnh.

#### Nội Dung

1. [S3 Bucket và CloudFront](1-S3-And-CloudFront/)
2. [Hàm Lambda](2-Lambda/)
3. [API Gateway](3-API-Gateway/)


#### Kiến trúc tổng quan

![Image](../images/Workshop_000002.drawio.png)
