---
title: "Clean Up Resources"
date: 2026-06-21
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

# Step 6: Clean Up Resources

### Objective

After completing the workshop, you need to delete the resources you created to avoid unnecessary charges.

---

### 1. Delete the SQS Queue

1. Go to Amazon SQS.

2. Select the queue created in the workshop, then choose Delete.

![Delete SQS queue](./images/image1.png)

3. Enter Confirm to confirm deletion.

![Confirm SQS queue deletion](./images/image2.png)

---

### 2. Delete the Lambda Function

1. Go to AWS Lambda.

2. Select the function created in the workshop, then choose Delete.

![Delete Lambda function](./images/image3.png)

3. Enter confirmation to delete the function.

![Confirm Lambda function deletion](./images/image4.png)

---

### 3. Delete the S3 Bucket

1. Go to Amazon S3.

2. Open the bucket created in the workshop.

3. Select the bucket to delete, then choose Delete.

Note: The S3 bucket must be emptied before deletion. If the bucket still contains objects, delete them first.

![Delete S3 bucket](./images/image5.png)

---

### 4. Delete the IAM Role

1. Go to IAM.

2. Select Roles.

3. Select the IAM Role Lambda-ImageProcessing-Role created in the workshop, then delete the role.

![Delete IAM Role](./images/image6.png)
