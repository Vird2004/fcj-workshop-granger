---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Cara tiên phong ứng dụng AI chuyên biệt cho các công ty môi giới bảo hiểm doanh nghiệp với AWS

Bảo hiểm là ngành công nghiệp trị giá 8 nghìn tỷ đô la toàn cầu đang gánh nặng bởi các quy trình thủ công và tình trạng thiếu hụt nhân tài ngày càng trầm trọng. Cara cung cấp một giải pháp AI-native trên AWS, tự động hóa các quy trình back-office cho các công ty môi giới bảo hiểm.

Các đại lý bảo hiểm thường xuyên dành hàng giờ cho những tác vụ lặp đi lặp lại: hoàn thiện hồ sơ đăng ký, phân tích phạm vi bảo hiểm, nhập lại dữ liệu qua nhiều hệ thống, và chuyển tiếp thông tin giữa khách hàng và nhà bảo hiểm. Khi ngành này phải đối mặt với tình trạng thiếu hụt nhân tài kéo dài, các công ty môi giới cần mở rộng doanh thu mà không phải tăng nhân sự tương ứng.

Trong bài viết này, chúng tôi khám phá cách Cara, được xây dựng với sự hợp tác của AWS, giải quyết những thách thức này. Chúng tôi đi qua các quyết định thiết kế kỹ thuật và các dịch vụ AWS hỗ trợ giải pháp, đồng thời chia sẻ những kết quả đo lường được mà Cara đã mang lại cho các công ty môi giới doanh nghiệp.

---

## Thách thức: Tại sao AI phổ thông không đủ trong lĩnh vực bảo hiểm

Các công ty môi giới bảo hiểm hoạt động trong một môi trường được kiểm soát chặt chẽ. Mỗi giao dịch đòi hỏi sự chính xác, khả năng kiểm toán, và tuân thủ quy định. Dữ liệu liên quan bao gồm thông tin nhận dạng cá nhân (PII) nhạy cảm, hồ sơ tài chính, và chi tiết bảo lãnh.

Các công cụ AI phổ thông không được thiết kế cho sự phức tạp này. AI hiệu quả trong bảo hiểm phải hiểu được các mô hình dữ liệu và quy trình làm việc của môi giới theo lĩnh vực chuyên biệt. Nó còn phải xử lý các yêu cầu riêng của từng nhà bảo hiểm và các ràng buộc quy định, trong khi đáp ứng các tiêu chuẩn bảo mật doanh nghiệp.

Nhóm sáng lập của Cara đã trực tiếp chứng kiến những khoảng trống này. Vic Yeh, Nikhil Kansal và Jon Patel trước đây đã thành lập một công ty môi giới bảo hiểm kỹ thuật số. Họ đã mở rộng và bán lại công ty cho The McGowan Companies, một trong những tổ chức bảo hiểm tư nhân lớn nhất tại Mỹ.

Trong quá trình đó, nhóm đã xây dựng một AI copilot nội bộ được vận hành bởi các mô hình ngôn ngữ lớn (LLM). Copilot này giảm thời gian xử lý, cải thiện độ chính xác dữ liệu, và tối ưu hóa quy trình làm việc của đại lý. Được khuyến khích bởi mức độ áp dụng cao, họ đã mở rộng khái niệm này thành một sản phẩm độc lập: Cara.

---

## Tổng quan kiến trúc

Cara được xây dựng trên các dịch vụ AWS được chọn vì độ tin cậy, khả năng mở rộng và bảo mật.

### Tính toán và điều phối

Cara chạy trên Amazon Elastic Kubernetes Service (Amazon EKS) để điều phối container trên nhiều Availability Zone. EKS quản lý các microservice của Cara, bao gồm pipeline nhập liệu, engine quy trình làm việc, và lớp inference.

Kiến trúc này hỗ trợ mở rộng linh hoạt để xử lý nhu cầu trong các giai đoạn tái tục và bảo dưỡng cao điểm. Nó hỗ trợ hàng nghìn người dùng và quy trình đồng thời cho mỗi công ty môi giới. Khối lượng công việc của mỗi tổ chức chạy trong các namespace riêng biệt để cách ly tenant.

### AI và inference

Khả năng AI của Cara được vận hành bởi các LLM được lưu trữ trên Amazon Bedrock. Amazon Bedrock cung cấp quyền truy cập vào các foundation model thông qua một API được quản lý hoàn toàn. Điều này cho phép Cara chạy inference mà không cần quản lý cơ sở hạ tầng GPU. Cara sử dụng Amazon Bedrock cho một số khả năng cốt lõi:

- **Thông tin phạm vi bảo hiểm và báo giá** – so sánh báo giá của các nhà bảo hiểm, tóm tắt sự khác biệt về phạm vi, và làm nổi bật các điều khoản loại trừ hoặc khoảng trống.
- **Tự động hóa đơn và biểu mẫu** – điền chéo các biểu mẫu ACORD và biểu mẫu bổ sung sử dụng tài liệu nguồn, hồ sơ đăng ký trước đó và hướng dẫn của đại lý.
- **Tạo đề xuất và tái tục** – tạo ra các đề xuất có thương hiệu sẵn sàng gửi khách hàng và bảng tính tái tục.
- **Quy trình làm việc dựa trên kiến thức** – tham chiếu các hướng dẫn đặc thù của đại lý, khẩu vị rủi ro của nhà bảo hiểm, và lịch sử giao dịch để hướng dẫn quyết định.

### Bảo mật và cách ly dữ liệu

Bảo vệ dữ liệu là yêu cầu nền tảng cho các tổ chức bảo hiểm. Kiến trúc của Cara sử dụng triển khai theo từng tài khoản trên AWS. Dữ liệu và quy trình làm việc của mỗi công ty môi giới được cô lập trong các không gian làm việc chuyên dụng, bảo mật. Thiết kế này hỗ trợ tuân thủ các quy định ngành và cung cấp khả năng kiểm toán ở cấp độ tổ chức.

### Tích hợp

Cara tích hợp với các hệ thống quản lý đại lý (AMS) và công cụ quản lý quan hệ khách hàng (CRM) hàng đầu. Nó đồng bộ tài khoản, chính sách và tài liệu để giảm việc nhập dữ liệu trùng lặp. Các quy trình làm việc do AI điều khiển hoạt động trực tiếp trong các stack công nghệ môi giới hiện có, giúp giảm thiểu thay đổi đối với các hệ thống mà đại lý của họ đang sử dụng.

---

## Đặc điểm triển khai và vận hành

Một trong những mục tiêu thiết kế của Cara là nhanh chóng tạo ra giá trị. Các công ty môi giới doanh nghiệp có thể được onboard trong vài giờ và triển khai các quy trình làm việc tùy chỉnh trong vài ngày. Việc triển khai Cara trên EKS sử dụng các template được tham số hóa cho mỗi tenant mới, cấp phát namespace, storage và inference endpoint riêng biệt mà không cần thiết lập thủ công.

Trong môi trường production, cơ sở hạ tầng của Cara trên AWS cung cấp:

- **Tính khả dụng cao** – triển khai multi-AZ trên EKS với failover tự động.
- **Mở rộng linh hoạt** – Kubernetes Horizontal Pod Autoscaler điều chỉnh năng lực theo nhu cầu thực tế, hỗ trợ hàng nghìn người dùng đồng thời trong các giai đoạn cao điểm.
- **Bảo mật doanh nghiệp** – cách ly dữ liệu theo tenant, mã hóa khi lưu trữ và truyền tải, và tích hợp với AWS Identity and Access Management (AWS IAM).

---

## Kết quả đo lường được

Các quy trình làm việc do AI điều khiển của Cara đã mang lại kết quả định lượng cho các công ty môi giới bảo hiểm doanh nghiệp:

| Chỉ số | Kết quả |
| --- | --- |
| Thời gian tiết kiệm mỗi người dùng | ~10 giờ/tuần nhờ tự động hóa quy trình và truy xuất kiến thức theo ngữ cảnh |
| Tốc độ onboard | Công ty môi giới doanh nghiệp được onboard trong vài giờ; quy trình tùy chỉnh hoạt động trong vài ngày |
| Năng lực đồng thời | Hàng nghìn người dùng và quy trình đồng thời cho mỗi công ty môi giới |
| Mức độ áp dụng | Được sử dụng bởi hàng trăm công ty đại lý và môi giới bảo hiểm hàng đầu |

Những kết quả này đến từ tự động hóa quy trình đặc thù theo tổ chức và truy xuất kiến thức theo ngữ cảnh, phụ thuộc vào AI chuyên biệt lĩnh vực của Cara và cơ sở hạ tầng có khả năng mở rộng, bảo mật được cung cấp bởi AWS.

---

## Nhìn về phía trước

Ngành bảo hiểm vẫn đang ở giai đoạn đầu của quá trình ứng dụng AI. Khi nhu cầu doanh nghiệp tăng lên, Cara tiếp tục mở rộng các quy trình làm việc do AI điều khiển trên toàn bộ mảng bán hàng, dịch vụ và vận hành.

"Chúng tôi rất vui mừng được đẩy xa ranh giới của AI chuyên biệt lĩnh vực trong các ứng dụng bảo hiểm thực tế cùng với AWS," Vic Yeh, CEO của Cara, chia sẻ. "Mục tiêu của chúng tôi là giúp các chuyên gia bảo hiểm trở về với cốt lõi của ngành: những mối quan hệ."

---

## Kết luận

Trong bài viết này, chúng tôi đã chỉ ra cách Cara xây dựng một giải pháp AI chuyên biệt lĩnh vực cho các công ty môi giới bảo hiểm sử dụng Amazon EKS và Amazon Bedrock. Kiến trúc này cung cấp các không gian làm việc được cách ly theo tenant với khả năng mở rộng linh hoạt, hỗ trợ hàng nghìn người dùng đồng thời trong khi đáp ứng các yêu cầu bảo mật và tuân thủ của ngành bảo hiểm.

Để tìm hiểu thêm về việc xây dựng ứng dụng AI trên AWS, hãy truy cập AWS Architecture Center. Để bắt đầu với Amazon Bedrock, xem Getting started with Amazon Bedrock. Đối với Amazon EKS, xem Getting started with Amazon EKS.

Nguồn: <https://aws.amazon.com/blogs/machine-learning/how-cara-pioneers-domain-specific-ai-for-enterprise-insurance-brokerages-with-aws/>
