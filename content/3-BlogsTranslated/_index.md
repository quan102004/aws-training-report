---
title: "Blogs Posted"
date: 2026-06-30
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

###  [Blog 1 - Ransomware "Immune" Infrastructure Mindset on AWS](3.1-Blog1/)
This blog delves into analyzing the strategy of building an AWS architecture to defend against organized Ransomware attack campaigns. Instead of relying on expensive tools, the article emphasizes the importance of network infrastructure planning to automatically break the malware propagation chain within the first "golden 72 hours." The content dissects 4 vital checkpoints: (1) Using IAM Temporary Elevated Access to eliminate privilege escalation risks; (2) Deploying VPC Endpoints instead of NAT Gateways to isolate network flows and block connections to C&C servers; (3) Applying a "Shift-Left" mindset to integrate scanning tools directly into the CI/CD pipeline; and (4) Building a unified monitoring center based on the AWS SRA architecture. 

###  [Blog 2 - Secure Access Control for Multi-User RAG Applications](3.2-Blog2/)
This blog focuses on solving one of the most challenging problems when building internal Generative AI applications: controlling access permissions to RAG (Retrieval-Augmented Generation) documents for multiple departments on the same Knowledge Base. Instead of duplicating the knowledge base, which is costly, the article introduces a multi-layer security architecture (Defense-in-Depth) combining Amazon Bedrock and Amazon Verified Permissions. The authentication and authorization flow is divided into two independent checkpoints: Layer 1 uses API Gateway and Lambda Authorizer to block unauthorized requests at the door; Layer 2 uses a dynamic Metadata Filter passed to the RetrieveAndGenerate API to limit the LLM's reading scope. The entire authorization logic is centrally managed using the highly intuitive and secure Cedar policy language.

###  [Blog 3 - Data Segregation for Real-Time Analytics with Aurora & QuickSight](3.3-Blog3/)
This blog presents an excellent real-world case study from the Oldcastle APG group on implementing a Real-Time Analytics architecture. The article dissects how the engineering team synchronizes data from the core Infor Cloud ERP system to the Dashboard without degrading the performance of OLTP transactions. The highlight of the architecture lies in the complete segregation of the data flow through Infor Data Fabric, combined with a Network Load Balancer, RDS Proxy, and Amazon Aurora PostgreSQL to handle millions of transactions securely via Private Subnets. Finally, the article guides how to use Amazon QuickSight with its Embedded Integration mechanism to directly embed a dynamic Dashboard into the user interface.