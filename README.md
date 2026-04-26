---
title: Deploying a Simple Webapp For Choosing A Coffe Of The Month 
id: AWS-1
subject: aws
services: Github Actions, ECS Fargate, ECR, Secrets Manager, RDS, ALB, IGW, NAT Gateway, VPC, SGs, IAM
estimated-time: 60 minutes
last-updated: 2026-04-6
---

## Problem
A coffe chain needs to deploy a webapp for choosing a coffe of the month drink where customers can vote on it and needs to be deployed to AWS while adhereing to the AWS Well-Architected Framework such as Operational excellence,  Security, Reliability, Performance efficiency, Cost optimization and Sustainability.

## Solution

We will rely on Github Actions for simple CI/CD pipelines to build the docker container from the docker file in the code's directory and connect it to ECR as a container registery while relying on ECS Fargate for serverless container deployment and RDS for managed database servers and Secrets Manager for automated secrets rotation and ALB for load balancing while setting up SGs and IAM Roles for secure service access and Private/Public Multi-AZ VPCs for high availabilty and NAT Gateways for Private subnet access.

## Architecture Diagram

