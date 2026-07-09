---
title: "Blog 2: Secure Access Control for Multi-Tenant RAG Applications"
date: 2026-06-22
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

### [SECURITY/Architecture] Secure Access Control for Multi-Tenant RAG Applications with Amazon Bedrock and Verified Permissions

Hello community members,

Building internal Generative AI applications using RAG (Retrieval-Augmented Generation) is always an appealing yet challenging topic in terms of architecture and security. We all know that personalizing document access is mandatory (e.g., HR personnel should only see HR documents, Sales see Sales documents), but implementing this authorization flow in practical infrastructure is far from simple.

Many systems today resort to creating separate Knowledge Bases for each department. The biggest drawback of this approach is the bloated duplication of infrastructure, skyrocketing maintenance costs, and a management nightmare when organizational changes occur.

Recently, while researching cloud networking architectures and data security patterns, I wanted to introduce an approach that completely resolves this bottleneck. Instead of physical segregation, we can use a single unified Knowledge Base and control access by combining **Amazon Bedrock** and **Amazon Verified Permissions**.

#### Defense-in-Depth Security Architecture

![Multi-Tenant RAG Security Architecture](/images/3-Blog/blog_2.jpg)
The core concept of this architecture is to completely decouple authorization logic from the application source code and apply security automation at two independent layers:

* **1. Layer 1 (API Access) - Edge Gatekeeping:** When a user sends a request, it does not query the database directly. Amazon API Gateway invokes a Lambda Authorizer to check with Verified Permissions whether the user (based on groups in their JWT token) is authorized to call the API. If invalid, the request is rejected immediately, reducing the risk of direct attacks.
* **2. Layer 2 (Document Access) - Root-Level Data Filtering:** If the user passes the first gate, a Middleware Lambda invokes Verified Permissions a second time to determine exactly which departments' documents the user is allowed to access. Based on this decision, the system automatically constructs a Metadata Filter and passes it directly to Amazon Bedrock's `RetrieveAndGenerate` API. Consequently, the Large Language Model (LLM) can only search and generate answers from strictly scoped documents. Even if Layer 1 is accidentally misconfigured, Layer 2 still prevents cross-tenant data leakage.

#### Centralized Policy Management with Cedar
The entire authorization logic is written in the intuitive **Cedar** policy language. When granting access to a new department or an executive, we only need to update policies in the console without rewriting code or redeploying the application. The system strictly adheres to the "Deny-by-default" principle, automatically blocking access if the authorization service fails.

This approach enables organizations to rapidly deploy a secure GenAI application serving dozens of departments while minimizing operational costs.

To better understand the practical implementation, the AWS Architecture Blog post analyzes this architectural pattern in high quality. If you are planning to build or upgrade an internal AI system, I highly recommend reading the original post to capture the deeper technical aspects.

I hope this share brings useful perspectives for Cloud Networking and System Architecture professionals.

---
**References:**
* **Link to original post:** [Secure multi-tenant RAG with Amazon Bedrock and Verified Permissions](https://aws.amazon.com/vi/blogs/architecture/secure-multi-tenant-rag-with-amazon-bedrock-and-verified-permissions/)
* **Link to group post:** [Cộng đồng AWS Study Group FCAJ](https://www.facebook.com/groups/660548818043427/?multi_permalinks=2202713613826932)