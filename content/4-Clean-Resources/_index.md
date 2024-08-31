+++
title = "Clean Up Resources"
date = 2024
weight = 4
chapter = false
pre = "<b>4. </b>"
+++

## Contents

After completing the setup, if not in use, we should clean up the resources created in this tutorial to avoid incurring unnecessary charges.

#### Delete S3 Bucket

1. First, empty the S3 Bucket you want to delete. You can use the **Empty** button to clear all files instead of deleting them one by one.
   ![Image](../images/Clean%20Resources/S3_00.jpg)
2. Next, choose **Delete** and confirm the deletion.
   ![Image](../images/Clean%20Resources/S3_03.jpg)

#### Delete Lambda Function

![Image](../images/Clean%20Resources/Lambda_1.jpg)

#### Delete CloudFront

1. Before deletion, disable the distribution you want to delete. (This process may take a few minutes.)
   ![Image](../images/Clean%20Resources/CF_1.jpg)
   ![Image](../images/Clean%20Resources/CF_3.jpg)
2. Delete the distribution using the **Delete** button.
   ![Image](../images/Clean%20Resources/CF_4.jpg)

#### Delete API Gateway

1. Delete Stages.
   ![Image](../images/Clean%20Resources/APIGW_1.jpg)
2. Delete API.
   ![Image](../images/Clean%20Resources/APIGW_2.jpg)
