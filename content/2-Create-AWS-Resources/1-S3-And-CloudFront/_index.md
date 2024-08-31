+++
title = "Create S3 Bucket and CloudFront"
date = 2024
weight = 1
chapter = false
pre = "<b>2.1. </b>"
+++

## CONTENT

This step includes creating an **S3 Bucket** and **CloudFront** distribution to access and use the content.

- [CONTENT](#content)
    - [Create S3 Bucket](#create-s3-bucket)
    - [Upload and View Images/Files/Folders](#upload-and-view-imagesfilesfolders)
    - [Create CloudFront](#create-cloudfront)

#### Create S3 Bucket

1. In the search bar, search for S3 and select it to go to the S3 Bucket service console.
   ![Image](../../images/S3_Related/Console_1.jpg)
2. Click **Create bucket** to create a new S3 Bucket.
3. On the create S3 Bucket page, enter the desired Bucket name and select ACLs disabled in the Object Ownership section.
   ![Image](../../images/S3_Related/Name_ownership.jpg)

{{% notice note %}}
Select the ACLs (Access Control List) disabled option to configure the ownership of all files, folders, etc., in the S3 Bucket to this AWS account. All access and modifications to objects within are governed by **Policies** (IAM Policies and Permissions). This enhances privacy, security, and data safety.
{{% /notice %}}

4. Configure the **Public Access** and **Bucket Versioning** settings as default.
   ![Image](../../images/S3_Related/Access_version.jpg)

{{% notice note %}}
Blocking public access ensures security, interacting only through **CloudFront** and **API** (with authentication).
{{% /notice %}}

5. Configure **Tags**, **Default encryption**, and **Advanced settings** as default.
   ![Image](../../images/S3_Related/Encrytion_setting.jpg)
   ![Image](../../images/S3_Related/Advanced_setting.jpg)

6. Click **Create bucket**. Your S3 Bucket has been created successfully.
   ![Image](../../images/S3_Related/Console_2.jpg)

#### Upload and View Images/Files/Folders

1. Click the **Upload** button.
   ![Image](../../images/S3_Related/Upload_console_1.jpg)
2. Select **Add files/Add folder** according to the type of object you want to upload and click **Upload**.
   ![Image](../../images/S3_Related/Upload_console_2.jpg)
   Upload successful.
   ![Image](../../images/S3_Related/Upload_console_3.jpg)
   ![Image](../../images/S3_Related/Upload_console_4.jpg)
3. You can view the content (for images) or download it using the **Open** button.
   ![Image](../../images/S3_Related/Upload_console_5.jpg)

{{% notice note %}}
You can view/download using the URL at Object URL if you disable the Block Public Access option (at Bucket creation stage).
{{% /notice %}}

#### Create CloudFront

1. In the search bar, search for CloudFront and select it to go to the AWS CloudFront service interface. Click **Create distribution** to create a new Distribution.
   ![Image](../../images/CloudFront_Related/Console_1.jpg)
2. Select the Origin domain as the domain of the S3 Bucket created above. Choose OAC (Origin Access Control) for the S3 Bucket created.
   ![Image](../../images/CloudFront_Related/Console_2.jpg)
   _If OAC does not exist, click Create new OAC to create a new one._
   ![Image](../../images/CloudFront_Related/OAC_Create.jpg)
3. Follow the steps as shown below.
   ![Image](../../images/CloudFront_Related/Console_3.jpg)
   ![Image](../../images/CloudFront_Related/Console_4.jpg)
4. Click **Create distribution** to initialize.
5. On the next initialization screen, you will see a prompt to add a policy to grant **CloudFront** access to the content stored in the S3 Bucket. Click Copy policy and return to the S3 Bucket management interface.
   ![Image](../../images/CloudFront_Related/Console_5.jpg)
6. Select the created S3 Bucket, click the Permissions tab, scroll down to the Bucket policy section, and click **Edit**.
   ![Image](../../images/CloudFront_Related/S3_Policy.jpg)
7. Paste the copied Policy and click **Save changes**.
   ![Image](../../images/CloudFront_Related/S3_Policy_2.jpg)
8. Return to the details of the newly created CloudFront Distribution (displayed at the **Last modified** section). Copy the **Distribution domain name** of the distribution (used to access content on the Origin domain).
   ![Image](../../images/CloudFront_Related/Console_6.jpg)
9. Access/view/download content in the S3 Bucket by entering the URL + path to the file stored in S3 (add '/' for subfolders).
   ![Image](../../images/CloudFront_Related/Image_Show.jpg)

That completes the first step, creating an S3 Bucket and CloudFront to view/use content in the storage.
