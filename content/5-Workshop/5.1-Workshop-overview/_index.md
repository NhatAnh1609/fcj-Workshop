---
title: "Workshop Overview"
date: 2026-06-21
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Build an Asynchronous Image Processing Workflow Using Amazon S3, SQS, and AWS Lambda

### Workshop Summary

This workshop guides you through building an asynchronous image processing workflow based on the Event-Driven model on AWS, solving the problem of “many users uploading images at the same time” while keeping the system stable, scalable, and cost-controlled.

---

### Main Objectives

- Design an S3 → SQS → Lambda architecture to process images through a queue, preventing Lambda from being called excessively when many uploads happen simultaneously.
- Write Lambda (Python) to:
  - Receive messages from SQS (containing events from S3)
  - Download the image from S3
  - Call Amazon Rekognition to suggest labels and detect status (for example, damaged packages)
  - Call Amazon Textract to extract text from labels (tracking number, route information, phone number, etc.)
  - Write results to CloudWatch Logs for monitoring and testing

### What You Will Learn

- Why SQS is needed as a buffer between S3 and Lambda in a high-traffic system.
- How to configure an IAM Role based on the Least Privilege principle.
- How to create and configure:
  - S3 bucket and Event Notification
  - SQS Standard Queue with important settings (Visibility Timeout, retention, etc.)
  - Lambda Trigger from SQS and process each message (small batch size for easier observation)
- The end-to-end Testing & Validation process and cleanup of resources to avoid unnecessary costs.
