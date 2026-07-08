---
title: "Các bài blogs đã dịch"
date: 2026-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Tại đây liệt kê các blogs mà mình đã tìm hiểu và dịch trong quá trình thực tập, xoay quanh chủ đề kiến trúc serverless, ứng dụng GenAI trên AWS, và tự động hóa hạ tầng:

###  [Blog 1 - Xây dựng hệ thống Thần Số Học (LunaGENZ) trên kiến trúc Serverless AWS kết hợp GenAI](3.1-Blog1/)
Bài viết ghi lại quá trình team xây dựng LunaGENZ – hệ thống dùng AI luận giải Thần số học cá nhân hóa – trên kiến trúc serverless (Next.js/Amplify, API Gateway, Lambda, DynamoDB). Nội dung tập trung vào lý do chọn serverless để tối ưu chi phí, cách xử lý timeout khi gọi AI bằng Amazon SQS, lý do chọn Claude 3 Haiku qua Amazon Bedrock, cùng các thực hành về bảo mật (Secrets Manager) và CI/CD.

###  [Blog 2 - Cara tiên phong ứng dụng AI chuyên biệt cho các công ty môi giới bảo hiểm doanh nghiệp với AWS](3.2-Blog2/)
Bài viết giới thiệu Cara, một giải pháp AI-native trên AWS giúp tự động hóa các quy trình back-office cho công ty môi giới bảo hiểm. Bài viết phân tích vì sao AI phổ thông không đủ trong lĩnh vực bảo hiểm, kiến trúc dựa trên Amazon EKS (điều phối, cách ly theo tenant) và Amazon Bedrock (inference AI), cũng như các kết quả đo lường được về thời gian tiết kiệm và tốc độ onboard khách hàng.

###  [Blog 3 - Tự động hóa việc Provision Oracle Database@AWS bằng Terraform](3.3-Blog3/)
Bài viết tóm tắt cách dùng Terraform (Infrastructure as Code) để tự động hóa việc khởi tạo Oracle Database@AWS (ODB@AWS), bao gồm ODB Network, Exadata Infrastructure, VM Cluster và ODB Peering Connection. Bài viết cũng nêu rõ các điều kiện tiên quyết (onboarding với Oracle, liên kết tài khoản AWS-OCI) và lợi ích của IaC so với thao tác thủ công qua Console.
