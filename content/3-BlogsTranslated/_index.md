---
title: "Translated Blogs"
date: 2026-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Listed here are the blogs I researched and translated during my internship, centered around serverless architecture, GenAI applications on AWS, and infrastructure automation:

###  [Blog 1 - Building a Numerology System (LunaGENZ) on a Serverless AWS Architecture with GenAI](3.1-Blog1/)
This post documents the team's process of building LunaGENZ – an AI-powered system for personalized numerology readings – on a serverless architecture (Next.js/Amplify, API Gateway, Lambda, DynamoDB). It covers why we chose serverless to optimize costs, how we handled AI-call timeouts using Amazon SQS, why we chose Claude 3 Haiku via Amazon Bedrock, and our security (Secrets Manager) and CI/CD practices.

###  [Blog 2 - How Cara Pioneers Domain-Specific AI for Enterprise Insurance Brokerages with AWS](3.2-Blog2/)
This post introduces Cara, an AI-native solution on AWS that automates back-office processes for insurance brokerages. It examines why general-purpose AI falls short in the insurance industry, an architecture built on Amazon EKS (orchestration, tenant isolation) and Amazon Bedrock (AI inference), and the measurable results in time saved and customer onboarding speed.

###  [Blog 3 - Automating the Provisioning of Oracle Database@AWS with Terraform](3.3-Blog3/)
This post summarizes how to use Terraform (Infrastructure as Code) to automate the provisioning of Oracle Database@AWS (ODB@AWS), including the ODB Network, Exadata Infrastructure, VM Cluster, and ODB Peering Connection. It also outlines the prerequisites (onboarding with Oracle, linking AWS-OCI accounts) and the benefits of IaC compared to manual Console operations.
