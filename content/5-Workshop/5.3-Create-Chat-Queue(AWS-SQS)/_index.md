---
title: "Create an Amazon SQS Message Queue"
date: 2026-06-21
weight: 3
chapter: false
pre : " <b> 5.3. </b> "
---

# Step 2: Create an Amazon SQS Message Queue

### Introduction

Amazon SQS serves as the intermediary queue between Amazon S3 and AWS Lambda.

When users upload images to S3, S3 sends notifications to SQS. Lambda then reads messages from SQS and processes them gradually, making the system more stable when many images are uploaded at the same time.

---

### Procedure

1. Go to the AWS Console, open the Amazon SQS service, and choose Create queue.

![Find Amazon SQS](./images/image13.png)

2. Choose the queue type as Standard Queue.

Do not choose FIFO Queue for this workshop because the goal is asynchronous image processing with high scalability, without strict ordering requirements.

![Choose Standard Queue](./images/image14.png)

3. Name the queue image-processing-queue.

![Name the SQS queue](./images/image15.png)

4. Configure the important queue parameters.

![Configure SQS parameters](./images/image16.png)

![Review SQS configuration](./images/image17.png)

5. Choose Create queue to create the queue.

6. After creation, copy the queue ARN. This ARN will be used in the next step to configure the S3 Event Notification.

![Copy the SQS queue ARN](./images/image18.png)
