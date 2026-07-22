---
title: "Amazon FSx"
date: 2026-06-12
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
Mission-critical enterprise applications heavily rely on Oracle databases; therefore, ensuring continuous High Availability (HA) is mandatory. Traditional Oracle HA solutions often require complex clustering software, expensive shared storage systems, and specialized database administrators. These approaches often introduce *single points of failure* and create significant operational overhead.

By combining **Amazon FSx for NetApp ONTAP (FSxN)** with AWS automation services, this article guides you on how to build a high-availability Oracle database architecture that drastically minimizes recovery time.

## Solution Overview

This solution integrates multiple AWS services to create a comprehensive HA architecture:

* **Amazon FSx for NetApp ONTAP (Multi-AZ):** Provides durable shared storage for Oracle data files, software, and configurations. Data remains continuously available even when an EC2 instance is replaced.
* **Amazon EC2 Auto Scaling groups:** Automates instance lifecycle management. If an instance fails, it is replaced with a new, identically configured instance that automatically connects to the FSxN shared storage.
* **AWS Backup:** Creates Amazon Machine Images (AMIs) that capture the latest configuration state of the Oracle server (including software patches and settings).
* **AWS Lambda & Amazon EventBridge:** Extracts the AMI ID from the latest backup recovery points and automates system updates.
* **AWS Systems Manager (SSM) Parameter Store:** Stores the latest AMI ID to ensure the Auto Scaling group always uses the most up-to-date configuration when launching a replacement instance.

## Core Benefits

* **RTO (Recovery Time Objective):** Only 2–5 minutes with the latest Oracle configuration.
* **RPO (Recovery Point Objective):** Near-zero thanks to Multi-AZ synchronous replication.
* **Consistency:** Replacement instances always launch with the exact same Oracle server setup as the previous instance.
* **Automated AMI Management:** Scheduling AMI creation and updating the Parameter Store are fully automated with zero manual intervention required.

## Implementation Guide

1. **Step 1: Establish Shared Storage (FSxN)**  
   Create a shared storage space with continuous Multi-AZ data synchronization across two availability zones. Next, configure the network (iSCSI) so the servers can mount this shared volume.
2. **Step 2: Set Up EC2 Instance Protection (AWS Backup)**  
   Configure automated backup plans (AMI creation) for the active Oracle server using resource tags for identification.
3. **Step 3: Extract the Latest Backup ID (Lambda)**  
   Whenever Step 2 completes, an AWS Lambda function is automatically triggered to extract the AMI ID of the newly created backup.
4. **Step 4: Configure Systems Manager (SSM) Parameter Store**  
   The Lambda function from Step 3 automatically overwrites the latest AMI ID in the SSM Parameter Store, ensuring the system always locates the most up-to-date configuration.
5. **Step 5: Set Up Auto Scaling Group with Self-Healing**  
   Create a server management group with a strict rule to maintain exactly **1 running instance**. If the active server fails, the system reads the SSM Parameter Store for the latest AMI, launches a replacement server, automatically mounts the shared storage (FSxN), and starts the Oracle database.

---

> **Conclusion:** By combining FSxN Multi-AZ shared storage with automated AMI management using AWS Backup and Lambda, enterprises can achieve Oracle High Availability while maintaining configuration consistency. The system automatically recovers from failures within minutes, minimizing operational risks and ensuring continuous business operations.

![blog picture](/images/3-BlogsPosted/blog1.jpg)

Links: <https://aws.amazon.com/vi/blogs/architecture/building-highly-available-oracle-databases-with-amazon-fsx-for-netapp-ontap/> <br> <https://www.facebook.com/groups/660548818043427/user/100081065478266>
