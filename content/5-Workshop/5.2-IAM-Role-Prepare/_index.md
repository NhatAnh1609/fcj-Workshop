---
title: "Prepare the IAM Role for Lambda"
date: 2026-06-21
weight: 2
chapter: false
pre : " <b> 5.2. </b> "
---

# Step 1: Prepare the IAM Role for Lambda

### Introduction

The IAM Role is the permission that Lambda uses to access the AWS services required in the workshop, such as Amazon S3, Amazon SQS, Amazon Rekognition, and Amazon Textract.

In this step, you will create an IAM Role for Lambda and attach the necessary policies so that Lambda can read data, receive messages, and write logs during image processing.

---

### Procedure

1. Go to the AWS Console and open the IAM service.

![Find the IAM service](./images/image1.png)

2. Select Roles, then choose Create role.

![Select Roles and Create role](./images/image2.png)

3. In the Trusted entity type section, select AWS service.

4. In the Use case section, select Lambda, then choose Next.

![Select AWS service and Lambda](./images/image3.png)

5. Find and attach the policies needed for Lambda one by one.

![Find policy for Lambda](./images/image4.png)

![Select policy for Lambda](./images/image5.png)

![Attach AWSLambdaBasicExecutionRole](./images/image6.png)

![Attach AmazonS3ReadOnlyAccess](./images/image7.png)

![Attach AmazonSQSFullAccess](./images/image8.png)

![Attach Rekognition and Textract policies](./images/image9.png)

6. Name the role Lambda-ImageProcessing-Role, then choose Create role.

![Name the IAM Role](./images/image10.png)

![Create the IAM Role](./images/image11.png)

---

### Security Note

In real-world environments, rather than using AWS-managed policies, you should create a Custom Policy to limit permissions to only the specific bucket or queue needed.

This is a security best practice following the Least Privilege principle, meaning you grant only the permissions required and nothing extra.

![Custom policy following the Least Privilege principle](./images/image12.png)
