---
title: "Proposal"
date: 2026-01-01
weight: 2
chapter: false
pre: "  2.  "
---


LMS & AI Proctoring System
Serverless Learning Management and AI Proctoring System on AWS
### 1. Executive Summary
- The LMS & AI Proctoring System is a Learning Management System (LMS) combined with AI-powered exam proctoring, built on an event-driven architecture using the AWS cloud platform. The system comprehensively supports the online examination lifecycle: from course and exam creation to the test-taking process and result retrieval. The core differentiator of the platform is the application of AI for automated grading (multiple-choice and essays) and candidate behavior monitoring via webcam to detect cheating in real time. By leveraging a serverless architecture, the system optimizes operating costs, minimizes manual monitoring efforts, and ensures flexible scalability based on the number of candidates.

### 2. Problem Statement
*Current Problems*
Organizing online exams across many educational institutions faces major challenges in monitoring, making cheating easy to occur (looking up documents, having someone else take the exam). Instructors must spend significant manpower and time directly monitoring video feeds or manually grading essay papers. Additionally, traditional LMS systems are often disjointed, lack built-in proctoring mechanisms, and are prone to crashing when concurrent candidate traffic spikes during final exams.

*Solution*
- The project builds a unified platform integrating an LMS and an AI proctoring pipeline. The system uses Kinesis Video Streams to ingest candidate video feeds, passing them through the AWS AI ecosystem (Rekognition, Transcribe, Bedrock) to recognize faces, prohibited objects, and transcribe voice audio. Cheating data is risk-scored and stored at high speed on DynamoDB, while emergency alerts are dispatched via SNS.

*Objectives*
- Ensure fairness in online examinations, reduce workload for instructors, and provide a highly available infrastructure operating on a pay-as-you-go pricing model based on actual usage.

### 3. Solution Architecture
- The platform adopts an AWS Serverless architecture, maintaining a clear separation between the Frontend (Client), core LMS business logic (Backend), and the automated AI proctoring processing pipeline.

**AWS Services Used:**

- Frontend & Security: Amazon Route 53, AWS WAF, AWS Amplify.

- Authentication & API: Amazon Cognito (STUDENT/INSTRUCTOR role management), Amazon API Gateway.

- Core Compute & Integration: AWS Lambda (business logic processing), Amazon EventBridge, Amazon SQS, AWS Step Functions (AI workflow orchestration).

- Video & AI Proctoring: Amazon Kinesis Video Streams, Amazon Polly (reading questions/instructions), Amazon Rekognition, Amazon Transcribe, Amazon Bedrock.

- Data Persistence: Amazon Aurora DB (LMS data), Amazon S3 (raw video storage), Amazon DynamoDB (cheating log storage).

- Observability & Alerts: Amazon CloudWatch, AWS X-Ray, Amazon SNS (real-time alerts).

- Security & Governance: AWS IAM, AWS KMS, AWS Secrets Manager, AWS SAM/CDK (IaC).
![Architecture](/images/2-Proposal/platform_architecture.jpg)

### 4. Technical Implementation
- Technology & Infrastructure Requirements

- Frontend: ReactJS, Vite, Tailwind CSS. The interface is statically hosted on Amazon Amplify combined with S3 for asset storage.

- Backend & Pipeline: Fully processed through Amazon API Gateway (REST API) and AWS Lambda to support the event-driven model.

- Database: Relational data (courses, users) resides in Aurora DB; high-throughput read/write data during exams (monitoring logs) resides in DynamoDB.

- Non-functional Requirements

- API response time under 2 seconds under normal conditions.

- Latency for detecting and recording anomalous behavior in video/audio streams under 5 seconds.

- System capability to auto-scale with traffic, ensuring backup and disaster recovery support.

### 5. Cost Estimation
- Assuming the system serves a scale of 500 students, organizing 50 exam sessions/month, with each session averaging 45 minutes of video streaming. The platform requires zero hardware investment (0 VND).

Estimated Monthly AWS Infrastructure Cost:

- AWS Lambda (20,000 req, 512MB): 0 USD

- Amazon API Gateway (20,000 req): 0.02 USD

- Amazon DynamoDB (On-demand): 1.19 USD

- Amazon S3 (Video and media storage): 1.26 USD

- Amazon Kinesis Video Streams: 0.18 USD

- Amazon Rekognition: 4.09 USD

- Amazon Transcribe: 0.60 USD

- Amazon Bedrock: 8.64 USD

- Amazon CloudWatch (15 metrics): 4.50 USD

- Amazon SNS (10,000 req): 0 USD

- AWS Security (IAM Access Analyzer / KMS / Secrets Manager): 4.46 USD

- Amazon Cognito: 0.07 USD

**Total**: ~25.01 USD/month (approx. ~650,000 VND). <br>
**Annual Cost:** ~300.12 USD/year.

### 6. Risk Assessment
- Key Risk Matrix

- System Overload (Peak Hours): High impact, medium probability.

- Exceeded AWS Costs (Excessive AI Calls): Medium impact, high probability.

- Data Loss or Corruption: Critical impact, low probability.

- High-Tech Cheating (Deepfake): Medium impact, low probability.

- Mitigation & Contingency Strategies

- Utilize AWS WAF Rate Limiting and the inherent auto-scaling nature of Serverless to prevent overloads.

- Set up AWS Budgets and CloudWatch Billing Alarms to trigger alerts or throttles when costs reach thresholds.

- Enable Point-in-Time Recovery (PITR) on the database to safeguard against data loss incidents.

- Contingency Plan: If AWS AI services experience service interruptions, the system falls back automatically: allowing submission to proceed normally, temporarily disabling AI, and flagging the video stream for manual instructor review after the exam ends.

### 7. Expected Outcomes
- Technical Improvements
Successfully construct an end-to-end business workflow from question generation to online grading on the AWS Serverless platform. Eliminate latency in traditional monitoring, provide real-time alerts, and centrally manage all learning and examination data.

- Long-term Value
The solution provides a transparent educational environment, saving hundreds of working hours for instructors in proctoring and grading. The system architecture serves as a foundation for students to practice real-world Cloud skills, while easily scaling to add further features (such as AI-driven oral examination, personalized learning analytics) toward completing a true commercial product.