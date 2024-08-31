+++
title = "Requirements"
date = 2024
weight = 1
chapter = false
pre = "<b>1. </b>"
+++

**Contents:**

- [Have an AWS Account](#have-an-aws-account)
- [Use IAM Account for the Lab (Recommended)](#use-iam-account-for-the-lab-recommended)
- [Have Postman Installed](#have-postman-installed)

#### Have an AWS Account

1. Go to the [Amazon Web Service homepage](https://aws.amazon.com/).
2. Select **Sign In to the Console** at the top right corner.
   - **\*Note:** It might be **Create an AWS Account**.\*
3. Enter your account information and select **Continue**.
   - **\*Important:** Make sure you enter the correct information, especially the email.\*
4. Choose account type.
   - **\*Note:** Both Personal and Professional accounts have the same features.\*
5. Enter your company or personal information.
6. Read and agree to the [AWS Customer Agreement](https://aws.amazon.com/agreement/).
7. Select **Create Account** and **Continue**.

#### Use IAM Account for the Lab (Recommended)

{{% notice info %}}
If you are using an IAM Account, you can skip this step.
{{% /notice %}}

- In the search bar, type **IAM** and select **IAM**, then click on Users.
- If no User exists, select **Create user**.
- Enter the information, check the box **Provide user access to the AWS Management Console - optional**, then click **Next**.
- In the **Attach policies directly** section, search for **\*AdministratorAccess** and select it, then proceed to **Next**.
- Review the information and click **Create user**.
- Retrieve the account, password, and Console sign-in URL (you may save these) and use them to log in with the IAM User.

{{% notice note %}}
Create an **Access key** for the user to log in via CLI. (Select the user to create, go to the **Access key** section in **Security credentials**)
{{% /notice %}}

#### Have Postman Installed
