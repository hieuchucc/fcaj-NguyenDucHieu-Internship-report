---
title: "Workshop"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5. </b> "
---


# System Architecture and Deployment Solution for LMS & AI Proctoring on AWS

#### Overview

- AWS provides a comprehensive ecosystem with an Event-driven Architecture and Serverless model, enabling the flexible, secure, and cost-optimized construction of a learning management system integrated with automated AI-powered exam proctoring.

- In this report, we will dive deep into the technology stack, core AWS services, and deployment strategy to operate the LMS & AI Proctoring System.

- The system leverages a combination of specialized AWS services to concurrently handle LMS business logic, capture real-time video streams, and execute the AI pipeline.

+ *Frontend & Routing* - Deploys interactive web interfaces using ReactJS combined with AWS Amplify, protecting incoming traffic via Amazon Route 53 and AWS WAF.

+ *Core Services & AI* - Uses AWS Lambda for business logic processing, Amazon Kinesis Video Streams for video/audio ingestion, integrated with Amazon Rekognition, Amazon Transcribe, and Amazon Bedrock for fraud monitoring and automated grading.

#### Content

1. [Workshop overview](5.1-Workshop-overview/)
2. [Prerequiste](5.2-Prerequiste/)
3. [Demo](5.3-Demo/)