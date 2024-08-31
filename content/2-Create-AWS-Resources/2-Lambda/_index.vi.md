+++
title = "Tạo hàm Lambda"
date = 2024
weight = 2
chapter = false
pre = "<b>2.2. </b>"
+++

## Nội dung

Ở bước này sẽ tạo một Lambda Function với chức năng xóa tệp chỉ định trên S3 Bucket.
- [Nội dung](#nội-dung)
    - [Tạo IAM Role cho phép Lambda có thể tương tác với S3 Bucket đã tạo](#tạo-iam-role-cho-phép-lambda-có-thể-tương-tác-với-s3-bucket-đã-tạo)
    - [Tạo hàm Lambda](#tạo-hàm-lambda)


#### Tạo IAM Role cho phép Lambda có thể tương tác với S3 Bucket đã tạo

1. Vào IAM Role và nhấn **Create role** để tạo Role mới cho Lambda.
2. Chọn **AWS service**/**Lambda**, nhấn **Next**.
   ![Image](../../images/Lambda/Lambda_IAM.jpg)
3. Ở bước Add permissions tiếp tục nhấn **Next**.
4. Đặt tên cho Role và review lại các tùy chọn sau đó nhấn **Create role**.
   ![Image](../../images/Lambda/Lambda_IAM_2.jpg)
5. Chọn Role vừa tạo, nhấn Add permissions -> Create inline policy để tạo Policy tùy chỉnh cho Role.

_JSON policy:_

    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "S3Interact",
                "Effect": "Allow",
                "Action": [
                    "s3:PutObject",
                    "s3:DeleteObject",
                    "s3:DeleteObjectVersion",
                    "s3:ListBucket"
                ],
                "Resource": [
                    "arn:aws:s3:::<your_s3_bucket_name>/*"
                ]
            },
            {
                "Effect": "Allow",
                "Action": "logs:CreateLogGroup",
                "Resource": "*"
            },
            {
                "Effect": "Allow",
                "Action": [
                    "logs:CreateLogStream",
                    "logs:PutLogEvents"
                ],
                "Resource": [
                    "arn:aws:logs:*:*:log-group:/aws/lambda/*"
                ]
            }
        ]
    }

5. Chọn tab JSON và dán policy bên trên vào sau đó nhấn **Next**.
   ![Image](../../images/Lambda/Lambda_IAM_3.jpg)
6. Đặt tên và xem lại các tùy chọn, sau đó nhấn **Create policy**.
   ![Image](../../images/Lambda/Lambda_IAM_4.jpg)

#### Tạo hàm Lambda

1. Trên thanh tìm kiếm, tìm Lambda và nhấn chọn để vào giao diện dịch vụ AWS Lambda, sau đó nhấn **Create function**.
   ![Image](../../images/Lambda/Console_1.jpg)
2. Cấu hình các thông tin cơ bản cho Lambda function (tên, ngôn ngữ lập trình,...). Ở mục **Execution role**, chọn tùy chọn **Use an existing role** và nhấn chọn IAM Role chúng ta vừa tạo ở trên. Sau đó nhấn **Create function**.
   ![Image](../../images/Lambda/Console_2.jpg)

Đoạn code này có mục đích là xóa file chỉ định trong S3 bucket cụ thể. Với 2 biến *bucketName* và *objectKey* được lấy từ path parameter trong url.

    import { S3Client, DeleteObjectCommand } from "@aws-sdk/client-s3";

    export const handler = async (event) => {
        const bucketName = event['pathParameters']['bucket'];  
        const objectKey = event['pathParameters']['key'];     

        const s3 = new S3Client();

        try {
            const command = new DeleteObjectCommand({
                Bucket: bucketName,
                Key: objectKey
            });

            await s3.send(command);

            console.log(`Successfully deleted ${objectKey} from ${bucketName}`);
            return {
                statusCode: 200,
                body: JSON.stringify({
                    message: `Deleted object ${objectKey} successfully`
                })
            };
        } catch (error) {
            console.error(`Error deleting object ${objectKey} from ${bucketName}:`, error);
            return {
                statusCode: 500,
                body: JSON.stringify({
                    message: `Failed to delete object`,
                    error: error.message
                })
            };
        }
    };


3. Dán mã nguồn bên trên vào phần Code của Lambda function vừa tạo rồi nhấn **Deploy**.
    ![Image](../../images/Lambda/Lambda_Func_1.jpg)

Chúng ta vừa hoàn thành bước tạo Lambda function có chức năng xóa một object trong S3 Bucket.