---
title : "CV Storage with Presigned URLs"
date : "2026-07-06"
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

#### Private S3 bucket + KMS

Bucket `job-tracker-cv-tqt-2026` with **Block all public access fully enabled**, encrypted with **SSE-KMS** (AWS managed key `aws/s3`, Bucket Key enabled to reduce KMS call costs). CORS only allows PUT/GET from the frontend domain.

#### Flow 7a–7b: direct upload/download

1. The client calls `POST /jobs/{jobId}/cv-url` with a JWT → the Lambda verifies the job belongs to that user → signs a **Presigned URL** valid for 5 minutes
2. The client PUTs/GETs **directly to S3** with that URL — the file never passes through Lambda, reducing load and cost

CVs are stored under the key `userId/jobId/file-name.pdf` — one private "compartment" per user. Only `.pdf` files are accepted, and the Content-Type is locked to `application/pdf` in the signature.

![CV uploaded](/images/capstone/s3-cv-uploaded.png)

#### Security verification

Accessing the **raw Object URL** (no signature) returns `AccessDenied`; only a valid Presigned URL can open the file:

![AccessDenied on raw URL](/images/capstone/s3-access-denied.png)

{{% notice tip %}}
**Lesson learned when testing Presigned URLs in Postman**: the PUT request to S3 must have the **Bearer token disabled** (the signature is already in the URL — two auth mechanisms at once get rejected by S3) and the `Content-Type` header must exactly match the signed value.
{{% /notice %}}
