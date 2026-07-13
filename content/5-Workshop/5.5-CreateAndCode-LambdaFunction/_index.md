---
title: "Create and Write Code for AWS Lambda"
date: 2026-06-21
weight: 5
chapter: false
pre : " <b> 5.5 </b> "
---

# Step 4: Create and Write Code for AWS Lambda

### Objective

In this step, you will create a Lambda Function to receive messages from Amazon SQS, read information about images uploaded to Amazon S3, and call AI services such as Amazon Rekognition and Amazon Textract to analyze the images.

---

### 4.1 - Create the Lambda Function

1. Go to AWS Lambda and choose Create function.

![Access AWS Lambda](./images/image1.png)

2. Choose Author from scratch.

![Choose Author from scratch](./images/image2.png)

![Create Lambda function](./images/image3.png)

3. Configure the Lambda Function.

![Configure Lambda function](./images/image4.png)

![Choose runtime and role](./images/image5.png)

Suggested configuration:

- Function name: image-quality-processor
- Runtime: Python 3.x
- Execution role: choose the IAM Role Lambda-ImageProcessing-Role created in Step 1

4. Choose Create function.

![Create function](./images/image6.png)

5. Open the Configuration tab, select General configuration, and choose Edit.

![Open General configuration](./images/image7.png)

6. Set Timeout = 60 seconds, then save the configuration.

![Set Lambda timeout](./images/image8.png)

---

### 4.2 - Attach SQS as a Trigger

1. On the Lambda Function page, choose Add trigger.

![Add trigger for Lambda](./images/image9.png)

2. Choose SQS as the source.

![Choose SQS trigger](./images/image10.png)

3. Select the image-processing-queue.

4. Configure Batch size = 1.

A batch size of 1 helps Lambda process one message at a time, which is suitable for the lab because it makes logs and debugging easier.

5. Choose Add.

![Configure SQS trigger](./images/image11.png)

---

### 4.3 - Write the Python Code

1. Open the Code tab.

2. Delete the sample code, paste the Python code that processes SQS messages, then choose Deploy to save the code.

![Write Lambda code and Deploy](./images/image12.png)

Sample code:

```python
import json
import urllib.parse

import boto3

s3 = boto3.client("s3")
rekognition = boto3.client("rekognition")
textract = boto3.client("textract")


def lambda_handler(event, context):
    for record in event["Records"]:
        body = json.loads(record["body"])

        for s3_record in body.get("Records", []):
            bucket = s3_record["s3"]["bucket"]["name"]
            key = urllib.parse.unquote_plus(s3_record["s3"]["object"]["key"])

            print(f"Processing image: s3://{bucket}/{key}")

            labels = rekognition.detect_labels(
                Image={
                    "S3Object": {
                        "Bucket": bucket,
                        "Name": key
                    }
                },
                MaxLabels=10,
                MinConfidence=70
            )

            print("Rekognition labels:")
            for label in labels["Labels"]:
                print(f"- {label['Name']}: {label['Confidence']:.2f}%")

            text_result = textract.detect_document_text(
                Document={
                    "S3Object": {
                        "Bucket": bucket,
                        "Name": key
                    }
                }
            )

            print("Textract text:")
            for block in text_result["Blocks"]:
                if block["BlockType"] == "LINE":
                    print(block["Text"])

    return {
        "statusCode": 200,
        "body": "Processed SQS messages successfully"
    }
```
