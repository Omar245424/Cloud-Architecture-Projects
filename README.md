---
Title: Deploying a Simple Webapp For Choosing Coffe Of The Month  
ID: AWS-1
Subject: aws
Services: Github Actions, ECS Fargate, ECR, Secrets Manager, RDS, ALB, IGW, NAT Gateway, VPC, SGs, IAM
Estimated-Time: 60 minutes
Last-Updated: 2026-04-6
---

## Problem
A coffe chain needs to deploy a webapp for choosing a coffe of the month drink where customers can vote on it and needs to be deployed to AWS while adhereing to the AWS Well-Architected Framework such as Operational excellence,  Security, Reliability, Performance efficiency, Cost optimization and Sustainability.

## Solution

We will rely on Github Actions for simple CI/CD pipelines to build the docker container from the docker file in the code's directory and connect it to ECR as a container registery while relying on ECS Fargate for serverless container deployment and RDS for managed database servers and Secrets Manager for automated secrets rotation and ALB for load balancing while setting up SGs and IAM Roles for secure service access and Private/Public Multi-AZ VPCs for high availabilty and NAT Gateways for Private subnet access.

## AWS Well-Architected Framework

To design a web application infrastructure according to the AWS Well-Architected Framework , We should adopt a Three-Tier Architecture. This separates our presentation, application, and data layers to maximize security, reliability, and scalability. 


1. Reliability: High Availability & Scaling 

The How: Deploy our app across multiple Availability Zones (AZs). Use an Application Load Balancer (ALB) to distribute traffic to Amazon ECS with Fargate containers.

The Why: If one data center (AZ) fails, our app remains online. Auto Scaling ensures we have exactly the resources needed to handle traffic spikes.
Database: Use Amazon RDS Multi-AZ or Amazon Aurora with a primary and secondary instance. This provides automatic failover if the primary database goes down. 

2. Security: Defense in Depth

The How:VPC Subnets: Place our web/app servers and database in private subnets with no direct internet access. Only the ALB should sit in a public subnet.
Security Groups: Implement the "Principle of Least Privilege." Our database security group should only allow inbound traffic from the application layer's security group on a specific port (e.g., 3306 for MySQL). Use AWS Secrets Manager to store secrets and auto rotate them automatically.

The Why: This minimizes the "attack surface." Even if one layer is compromised, the rest of your infrastructure remains isolated and our secrets are highly secured and not hard coded in our app's code. 

3. Performance Efficiency: Purpose-Built Services

The How: Use Amazon ECS Fargate as a Container Orcherstration Engine for Handling our Containers and ECR for Storing our Containers.

The Why: This reduces manaual intervention in the scaling and healing of our app's code as well as reduces operational overhead.
Database Choice: Use a purpose-built data store. For relational data, use RDS.

4. Operational Excellence: Infrastructure as Code (IaC)

The How: Deploy our infrastructure using Terraform instead of clicking in the console. Implement a CI/CD pipeline using Github Actions.

The Why: IaC makes our environment "repeatable" and "version-controlled." If we need to recreate our stack in another region or recover a failed infrastructure in minutes instead of days, we just run a script. 

5. Cost Optimization: Pay only for what you use 

The How: Use Serverless options where possible, such as ECS Fargate for serverless cotainers orcherstration without the overhead of managing or wasting resources on over provisioned VMs.

The Why: Serverless scales down when no one is using our app, meaning we don't pay for over provisioned VMs. 

6. Sustainability: Efficient Energy Use

The How: Right-size our resources. Monitor utilization with Amazon CloudWatch and decommission unused resources.

The Why: Running fewer, more efficient servers reduces the total carbon footprint of your cloud workload.

## Architecture Diagram
<img width="1280" height="720" alt="Slide1" src="https://github.com/user-attachments/assets/85fc2d63-bb74-422a-9a1d-8e98560e2b8c" />


