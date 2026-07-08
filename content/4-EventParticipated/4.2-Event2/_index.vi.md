---
title: "Event 2"
date: 2026-06-06
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch “Meeting 06/6”

### Mục Đích Của Sự Kiện

- Khám phá các công nghệ và giải pháp đám mây chuyên sâu (Docker, AWS WAF, WebSocket, GraphRAG).
- Học hỏi kinh nghiệm thực tế từ lộ trình phát triển sự nghiệp trong ngành IT.
- Nâng cao kỹ năng làm việc nhóm (Teamwork) và bảo mật hệ thống.

### Danh Sách Diễn Giả

- **Bảo Huỳnh** - Docker - A containerization technology
- **Lê Hoàng Gia Đại** - Combining AWS WAF with Machine Learning for Cyber Attack Detection
- **Nguyễn Quốc Bảo** - Multiplayer in the Cloud Connecting Godot Clients with AWS WebSockets
- **Trương Huy Phước** - The art of effective teamwork
- **Trần Trung Vinh** - From IT Helpdesk to Senior Sysadmin
- **Việt Phát** - Build GraphRAG applications using Amazon Bedrock and Amazon Neptune

### Nội Dung Nổi Bật

#### Docker - A containerization technology

- Sự khác biệt giữa Ảo hóa (Virtualization) và Container hóa: Container nhẹ hơn, tiết kiệm tài nguyên và khởi động nhanh hơn máy ảo (VM).
- Lợi ích của Docker: Chạy ổn định trên nhiều môi trường, dễ dàng di chuyển, lý tưởng cho kiến trúc Microservices.
- Kiến trúc Docker: Cách hoạt động của Docker Image, Container và quy trình tạo ra một Image từ Dockerfile bằng các lệnh cơ bản.
- Ứng dụng thực tế: CI/CD, phát triển ứng dụng Cloud-native và hiện đại hóa hệ thống cũ.

#### Combining AWS WAF with Machine Learning for Cyber Attack Detection

- Giới hạn của WAF truyền thống: Phụ thuộc vào các luật (rules) có sẵn, khó phát hiện các cuộc tấn công Zero-day hoặc hành vi bất thường mới.
- Giải pháp kết hợp WAF và Machine Learning (NIDS): Hệ thống tự động học hỏi từ dữ liệu mạng để phát hiện các mẫu tấn công mới mà không cần định nghĩa sẵn rule.
- Quy trình huấn luyện mô hình: Sử dụng tập dữ liệu CSE-CIC-IDS2018, xử lý dữ liệu, cân bằng nhãn (labels) và huấn luyện bằng mô hình LightGBM.
- Triển khai thực tế: Kiến trúc hệ thống trên AWS kết hợp ALB, WAF, S3, Kinesis, Lambda và bảng điều khiển (Dashboard) theo dõi thời gian thực.

#### Multiplayer in the Cloud Connecting Godot Clients with AWS WebSockets

- So sánh các kiến trúc mạng trong game: UDP (nhanh nhưng phức tạp), WebSocket (phù hợp với game theo lượt, độ trễ thấp, tin cậy), HTTP Polling (đơn giản nhưng độ trễ cao).
- Kiến trúc giải pháp AWS: Sử dụng API Gateway (WebSocket), Lambda Function và DynamoDB để quản lý kết nối và trạng thái của người chơi.
- Tích hợp Godot Client: Cách xử lý các sự kiện `$connect`, `$disconnect`, và `$default` để trao đổi dữ liệu JSON trong thời gian thực.
- Bài học kinh nghiệm: Xử lý các kết nối "chết" (GoneException), chi phí quét bảng DynamoDB (Scan Cost) và trạng thái của Lambda (Stateless).

#### The art of effective teamwork

- Quy tắc 1: Có mục tiêu rõ ràng và chung (Clear & Shared Goals).
- Quy tắc 2: Sắp xếp đúng người, đúng việc (Right Person, Right Place).
- Quy tắc 3: Giao tiếp cởi mở và lắng nghe tích cực (Open Communication & Active Listening).
- Quy tắc 4: Trách nhiệm cá nhân (Personal Accountability).
- Công cụ hỗ trợ: Trello, ClickUp, Google Workspace, Slack, Discord.

#### From IT Helpdesk to Senior Sysadmin

- Vai trò của IT Helpdesk: Rèn luyện khả năng xử lý sự cố dưới áp lực, tư duy giải quyết vấn đề và giao tiếp với người dùng.
- Công việc của System Admin: Quản lý hạ tầng máy chủ, bảo mật, vá lỗi, theo dõi hệ thống. Tuyệt đối không "test in production".
- Chuyển mình lên Cloud/DevOps: Tư duy về Cloud (AWS, Elastic scaling), Infrastructure as Code (Terraform) và văn hóa DevOps (CI/CD, Docker, Tự động hóa).
- Bài học cốt lõi: Tập trung chuyên sâu vào 1-2 kỹ năng cốt lõi, xây dựng dự án thực tế quan trọng hơn chỉ có chứng chỉ, và đừng sợ thất bại.

#### Build GraphRAG applications using Amazon Bedrock and Amazon Neptune

- Khái niệm RAG: Tăng cường cho LLM bằng cách truy xuất thông tin từ cơ sở tri thức bên ngoài.
- GraphRAG là gì: Sử dụng đồ thị tri thức (Knowledge Graph) để thực hiện tư duy nhiều bước (Multi-hop Reasoning) và nhận diện các mối quan hệ rõ ràng giữa các thực thể.
- Lộ trình Fully Managed: Sử dụng Amazon Bedrock Knowledge Bases và Amazon Neptune Analytics để trích xuất thực thể, tạo nhúng (embeddings) và lưu trữ đồ thị.
- Lộ trình Custom: Dùng LlamaIndex kết hợp với Neptune để chuẩn bị dữ liệu, tạo đồ thị tri thức và truy vấn Cypher.

### Trải nghiệm trong event

Tham gia sự kiện "Meeting 06/6" giúp tôi mở rộng tầm nhìn về việc kết hợp các công nghệ Cloud tiên tiến vào thực tiễn:

- **Kiến thức kỹ thuật chuyên sâu:** Tôi đã học được cách kết hợp Machine Learning với AWS WAF để bảo mật tự động, cách triển khai game nhiều người chơi bằng WebSocket trên AWS và sự khác biệt rõ rệt giữa Docker và máy ảo truyền thống.
- **Cập nhật xu hướng AI:** Hiểu được sức mạnh của GraphRAG trong việc nâng cao khả năng phân tích và trả lời của AI nhờ vào Amazon Bedrock và Neptune.
- **Định hướng nghề nghiệp:** Câu chuyện từ Helpdesk lên Senior Sysadmin đã truyền cảm hứng rất lớn, giúp tôi nhận ra tầm quan trọng của việc xây dựng năng lực qua các dự án thực tế.
- **Kỹ năng mềm:** Các quy tắc về làm việc nhóm hiệu quả là hành trang không thể thiếu trong các dự án công nghệ phức tạp.


