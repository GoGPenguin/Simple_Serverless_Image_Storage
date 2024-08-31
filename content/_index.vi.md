+++
title = "Kho lưu trữ ảnh Serverless đơn giản với AWS S3"
date = 2024
weight = 0
pre = "<b>0. </b>"
chapter = false
+++

# Lưu trữ ảnh đơn giản với S3 Bucket

#### Tổng quan

Trong bài lab này, các bạn sẽ sử dụng và làm quen với các dịch vụ của AWS như **S3 Bucket**, **CloudFront**, **API Gateway**, **Lambda** để tự tạo một kho lưu trữ ảnh đơn giản. Tương tác với các dữ liệu trong S3 Bucket thông qua **REST API**.

#### S3 Bucket

Amazon S3 (Simple Storage Service) là một dịch vụ lưu trữ đối tượng (object storage) của Amazon Web Services (AWS).

#### CloudFront

Amazon CloudFront là một dịch vụ phân phối nội dung (Content Delivery Network - CDN) của Amazon Web Services (AWS). CloudFront giúp cải thiện hiệu suất và tốc độ tải trang web, ứng dụng, và nội dung bằng cách phân phối các đối tượng (như tệp tin, hình ảnh, video) từ các vị trí gần với người dùng cuối (các **Edge locations**).

#### Lambda

AWS Lambda là một dịch vụ điện toán serverless (không máy chủ) của Amazon Web Services (AWS). Lambda cho phép bạn chạy mã mà không cần phải quản lý máy chủ hoặc cấu hình cơ sở hạ tầng.

#### API Gateway

Amazon API Gateway là một dịch vụ của Amazon Web Services (AWS) giúp bạn dễ dàng tạo, triển khai, và quản lý các API (Application Programming Interface) cho ứng dụng và dịch vụ.

#### Nội dung chính

1. [Yêu cầu](1-Prerequisites/)
2. [Tạo các tài nguyên AWS](2-Create-AWS-Resources/)
3. [Thử nghiệm API với Postman](3-Test-API/)
4. [Dọn dẹp tài nguyên](4-Clean-Resources/)
