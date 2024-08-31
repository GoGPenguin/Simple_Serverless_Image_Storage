+++
title = "Create Lambda Function"
date = 2024
weight = 2
chapter = false
pre = "<b>2.2. </b>"
+++

## Content

In this step, you will create a Lambda Function to delete a specified file from an S3 Bucket.
- [Content](#content)
    - [Create IAM Role to Allow Lambda to Interact with the Created S3 Bucket](#create-iam-role-to-allow-lambda-to-interact-with-the-created-s3-bucket)
    - [Create Lambda Function](#create-lambda-function)

#### Create IAM Role to Allow Lambda to Interact with the Created S3 Bucket

1. Go to IAM Roles and click **Create role** to create a new Role for Lambda.
2. Select **AWS service**/**Lambda**, then click **Next**.
   ![Image](../../images/Lambda/Lambda_IAM.jpg)
3. On the Add permissions step, click **Next**.
4. Name the Role and review the options, then click **Create role**.
   ![Image](../../images/Lambda/Lambda_IAM_2.jpg)
5. Select the created Role, click Add permissions -> Create inline policy to create a custom Policy for the Role.

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

5. Select the JSON tab and paste the policy above, then click **Next**.
   ![Image](../../images/Lambda/Lambda_IAM_3.jpg)
6. Name and review the options, then click **Create policy**.
   ![Image](../../images/Lambda/Lambda_IAM_4.jpg)

#### Create Lambda Function

1. In the search bar, search for Lambda and select it to go to the AWS Lambda service interface, then click **Create function**.
   ![Image](../../images/Lambda/Console_1.jpg)
2. Configure the basic information for the Lambda function (name, programming language, etc.). In the **Execution role** section, select **Use an existing role** and choose the IAM Role you created earlier. Then click **Create function**.
   ![Image](../../images/Lambda/Console_2.jpg)

This code is intended to delete a specified file in a specific S3 bucket. The variables *bucketName* and *objectKey* are retrieved from the path parameters in the URL.

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

3. Paste the above code into the Code section of the Lambda function you created, then click **Deploy**.
    ![Image](../../images/Lambda/Lambda_Func_1.jpg)

You have now completed the step of creating a Lambda function to delete an object in an S3 Bucket.
