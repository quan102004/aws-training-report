---
title: "Event 3 - FCAJ Community Day June 2026"
date: 2026-06-27
weight: 4
chapter: false
pre: " <b> 4.3. </b> "
---

| Info | Details |
|---|---|
| Date | 27/06/2026 |
| Location | Floor 26, Bitexco Financial Tower, Sài Gòn Ward, Ho Chi Minh City |
| Role | Attendee |

This page summarizes the content from the **FCAJ Community Day in June 2026**, focusing on practical solutions: integrating AI into system operations, optimizing infrastructure, and securing data at enterprise scale.

---

### Summary of Key Presentation Topics

| Speaker | Topic | Core Technical Keywords |
|---|---|---|
| Steve Tran | Cloud Infrastructure Operations and the Agentic Platform Era | Agentic Platform, Multi-Agent, FinOps, Incident Investigation |
| Hieu Nghi, Kiet, Trung | Building Voice AI Assistant for Enterprise | STT, TTS, Bedrock Agent Core, Tool Calling |
| Bao & Nguyen Nguyen (Cloud Kinetics) | Implementing DevOps AI Agent on AWS | DevOps Agent, MCP, Topology, RCA |
| Truong & Minh Anh (Noventic) | Automating HR Processes with Amazon Q | Amazon Q, CV Screening, Token Optimization, No-code App |
| Toan Nguyen & Hieu Nghi (Renova Cloud) | Private Security for Amazon Q and MCP Server | VPC Connection, Private Subnet, Route 53 Resolver, ALB, Zero Trust |

---

### 1. Steve Tran (Cloud Thinker) - Cloud Infrastructure Operations and the Agentic Platform Era

As enterprises shift to Microservices architecture, systems grow larger and more complex. The speaker pointed out that current operations teams are overloaded by fragmented Observability tools, compounded by accumulated technical debt from legacy systems. An intelligent platform was introduced to help Senior engineers resolve incidents faster, minimizing system downtime.

**The Agentic Platform addresses 4 core problems:**

| Problem | Description |
|---|---|
| Incident Investigation | Automated high-speed incident investigation, reading system logs in minutes instead of hours |
| Code Reviews | Automated review of infrastructure code changes before Production deployment |
| FinOps | Cost optimization through deep understanding of both cloud infrastructure and business cash flow |
| Security | Simulating hacker behavior to automate Pentesting and system configuration assessment |

**Single Agent vs Multi-Agent:**
- **Single Agent**: When well-designed, can smoothly handle over 95% of tasks
- **Multi-Agent**: Advantages through task decomposition to Specialist agents, optimizing context capacity and Role-Based Access Control (RBAC)

---

### 2. Hieu Nghi, Kiet, and Trung - Step-by-Step Building a Voice AI Assistant for Enterprise

The Voice AI field in Vietnam presents a significant opportunity due to the relative scarcity of standardized voice training data. Two common architectural approaches were analyzed:

**Two approaches:**
- **Speech-to-Speech**: Direct audio-to-audio translation - very promising but currently only supports English well
- **STT + LLM + TTS** (Optimal solution for Vietnamese): Speech-to-Text converts voice to text, LLM processes context, Text-to-Speech responds with natural audio

**Advantages for enterprise environments (e.g. Banking):**
- Routing data through intermediate text format enables content control (Guardrails), minimizing AI misinformation
- The voice system can automatically call APIs (Tool calling) in real-time to perform tasks like card locking or customer identity verification

**Production challenges addressed:**
- Using Streaming to reduce latency
- Adding regional accent voice data
- Integrating gender recognition models for appropriate forms of address
- Handling random interruptions from users
- Automatically transferring calls to human agents when exceeding processing capability

---

### 3. Bao and Nguyen Nguyen (Cloud Kinetics) - Implementing DevOps AI Agent on AWS

In large-scale systems, engineers often spend significant time investigating incidents because monitoring data is scattered across different tools. The DevOps AI Agent solution fully automates this process immediately upon receiving error alerts from the system (e.g. CloudWatch) or direct requests from operations engineers.

**6 pillars of the DevOps Agent system:**

| Pillar | Description |
|---|---|
| Context Learning | Automatically learns system architecture through Agent Space to map visual Topology |
| Control | Strict permissions, precisely limiting the Agent's operational scope and resources |
| Integration | Extends data and infrastructure connectivity via MCP (Model Context Protocol) |
| Collaboration | Flexible connection with Slack, Jira, ServiceNow |
| Convenient | Simple, quick activation directly on the AWS Console |
| Cost Effective | Transparent pricing based on actual task runtime (~$0.083/second) instead of per-token |

**4-step incident resolution process:**
1. Preliminary error classification
2. Root Cause Analysis (RCA) investigation
3. Quick remediation recommendation
4. Long-term improvement recommendation to prevent recurrence

> The DevOps Agent only provides specific remediation proposals for engineers to review and execute manually - it does not directly intervene in the Production environment.

---

### 4. Truong and Minh Anh (Noventic) - Automating HR Processes with Amazon Q

Traditional HR departments face the burden of manually screening large volumes of resumes, risking overlooking talent, with evaluation processes sometimes being subjective. Using public AI tools to analyze resumes always carries the risk of internal data leakage. Amazon Q solves this by providing an intelligent assistant platform within a secure internal environment.

**Connectivity:** Diverse integration with Microsoft Workspace, Google Workspace, Jira, Salesforce, GitHub through MCP protocol.

**Automated recruitment scenario demonstrated:**
1. System automatically analyzes instruction files to create a specialized "HR talent review assistant" capability
2. AI helps draft Job Descriptions (JD), automatically scans all resumes in a directory (including scanned image formats via OCR)
3. Matches and classifies candidates by fit level (Strong, Good, Low, Very Low) based on technical criteria
4. Suggests corresponding salary benchmarks and exports detailed assessment reports in HTML, managing application progress through a no-code application

---

### 5. Toan Nguyen and Hieu Nghi (Renova Cloud) - Private Security Model for Amazon Q and MCP Server

By default, applications like Amazon Q connect through the public internet. Opening Public endpoints when AI needs to interact with internal MCP Servers creates significant security risks such as DDoS and Man-in-the-middle attacks. Establishing a private security model following Zero Trust standards is critically important.

**Architecture solution:**
- Completely isolate MCP Server inside the VPC's Private Subnet
- Amazon Q establishes a secure Interface Endpoint through VPC Connection
- Traffic routed through ALB in the private network for TLS encryption
- Combined with AWS Certificate Manager (ACM) and authentication via Amazon Cognito
- Route 53 Resolver manages all internal DNS for MCP Server within the VPC, ensuring server addresses are completely hidden from the external internet

**Estimated operational cost:** $250 - $350/month

---

### 6. Photo from the Event

![Photo from Event 3](/images/4-Event/4.3-Event3/event3-photo.png)
![Photo from Event 3](/images/4-Event/4.3-Event3/event3-photo2.png)

---

### 7. Conclusion

The FCAJ Community Day June 2026 event delivered a clear message: **The real value of AI lies in how the ecosystem and operational processes are designed around it**, not just in the technology model itself.

| Audience | Key Message |
|---|---|
| Engineers / Individuals | AI is a powerful support and amplification tool, not a complete replacement for human roles |
| Enterprises | When deploying AI to Production, Data Governance, Guardrails, and Private Security are always prerequisites |
