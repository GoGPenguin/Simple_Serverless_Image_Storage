+++
title = "Create Required Resources"
date = 2024
weight = 2
chapter = false
pre = "<b>2. </b>"
+++

In this step, we will initialize the necessary resources.  
First, create an S3 Bucket to store images and a CloudFront distribution to access the stored images.  
The second step is to create a Lambda function with the capability to delete image files in S3 (Serverless).  
In the third step, we will create an API Gateway to interact with the S3 Bucket through the API and S3 Bucket Integration for uploading images.

#### Contents

1. [S3 Bucket and CloudFront](1-S3-And-CloudFront/)
2. [Lambda Function](2-Lambda/)
3. [API Gateway](3-API-Gateway/)

#### Overview Architecture

![Image](../images/Workshop_000002.drawio.png)
