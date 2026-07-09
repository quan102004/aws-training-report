---
title: "Blog 3: Real-Time Analytics with Amazon Aurora & QuickSight"
date: 2026-06-29
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

### [DATA/Architecture] Data Segregation for Real-Time Analytics: Lessons from Oldcastle with Amazon Aurora & QuickSight

Hello community members,

In manufacturing or logistics enterprises, operational data changes by the second. Extracting data from core ERP systems onto real-time dashboards without overloading or slowing down the production environment is always a headache in cloud architecture design.

A highly typical case study that fully addresses this issue, recently shared by AWS, is **Oldcastle APG** – a major building materials supplier in North America with over 150 facilities. When migrating their on-premises systems to Infor Cloud ERP on AWS, they encountered a major hurdle: the built-in reporting capabilities of Infor Cloud ERP only supported a very limited number of reports. Users across different departments had to wait for batch reports, causing serious delays in decision-making.

Instead of pointing BI tools directly at the production ERP database, Oldcastle chose a more optimized approach: **building an architecture that completely segregates data using Infor Data Fabric Stream Pipelines and AWS services.**

#### Battle-Tested Data Streaming Architecture
The idea here is to capture change data and push it out immediately. The processing flow is highly optimized:

* **Ingestion:** Infor Data Fabric streams modifications (insert, update, delete) immediately without waiting to save them to a data lake.
* **Handling Networking (Load Distribution):** Since the Infor system could not directly access the private VPC, they had to use a Network Load Balancer (NLB) with static Elastic IPs placed in a public subnet. Behind it, EC2 instances acting as RDS Routers used `iptables NAT rules` to securely forward traffic to the database located in the private subnet.
* **Connection Management:** With high-frequency data streaming, they deployed **Amazon RDS Proxy** between the router and database to manage the connection pool, absorb traffic spikes, and handle automatic failovers.
* **Flexible Storage:** Data lands in **Amazon Aurora PostgreSQL** (Multi-AZ deployment). A great technical choice here was storing the streaming data flow into `JSONB` columns for flexible queries, leveraging Aurora's native JSON functions when parsing is required.

#### Delivering Dashboards to Users' Fingertips
Once analyzed, the data needs to be displayed smoothly. **Amazon QuickSight** was chosen and leveraged SPICE in-memory engine to accelerate query speeds.

But the highlight is the **Embedded Integration** mechanism. Instead of forcing users to open a separate BI (Business Intelligence) link, they used Amazon API Gateway and AWS Lambda for authentication, then invoked the QuickSight API to generate dynamic URLs (complete with Row-Level Security configuration). As a result, these dashboards were embedded directly into the users' familiar Infor OS interface using `iframes`.

#### Impressive Real-World Results
* In just 8 months, they successfully deployed over **50 dashboards** and complex reports.
* The system supports over **100 concurrent users** and handles millions of transactions daily with no performance degradation.

> This is a textbook architecture pattern for anyone working with Cloud ERP, Data Analytics, or System Integration. Decoupling the analytical layer from the transactional (OLTP) system not only offloads processing from the ERP but also paves the way for advanced AI/ML capabilities in the future.

---
**References:**
* **Link to original post:** [Real-time analytics with Infor Cloud ERP and AWS services](https://aws.amazon.com/blogs/architecture/real-time-analytics-with-infor-cloud-erp-and-aws-services/)
* **Link to group post:** [Cộng đồng AWS Study Group FCAJ](https://www.facebook.com/groups/660548818043427/?multi_permalinks=2206817163416577)