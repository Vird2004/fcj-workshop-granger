---
title: "Blog 3"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Tự động hóa việc Provision Oracle Database@AWS bằng Terraform

Khi cần vận hành Oracle Database hiệu năng cao trên đám mây, Oracle Database@AWS (ODB@AWS) hiện là một trong những giải pháp mạnh mẽ nhất. Dịch vụ này mang Exadata – nền tảng phần cứng cơ sở dữ liệu tối ưu nhất của Oracle – đặt trực tiếp bên trong trung tâm dữ liệu của AWS. Nhờ đó, hệ thống đạt được độ trễ mạng cực thấp và khả năng tích hợp sâu sắc với các dịch vụ native của AWS như Amazon S3, AWS KMS, Amazon EC2, hay Amazon EKS.

Tuy nhiên, việc thiết lập thủ công một hạ tầng phức tạp bao gồm ODB Network, Exadata Infrastructure, cho đến VM Cluster thông qua giao diện Console tốn rất nhiều thời gian và tiềm ẩn nguy cơ sai sót cao. Đó là lý do vì sao Infrastructure as Code (IaC) với cụ thể là Terraform trở thành công cụ đắc lực giúp bạn tự động hóa toàn bộ quy trình này một cách đáng tin cậy.

Trong bài viết mới trên AWS Database Blog, hai tác giả Javeed Mohammed và Sharath Chandra Kampili đã hướng dẫn chi tiết cách hiện thực hóa giải pháp trên. Bài viết dưới đây sẽ tóm tắt lại các điểm cốt lõi và quy trình triển khai bằng code.

---

## 1. Tại sao nên chọn Terraform (IaC) cho Oracle Database@AWS?

Việc định nghĩa hạ tầng bằng mã nguồn (HCL) mang lại những lợi ích vượt trội cho doanh nghiệp:

- **Tự động hóa đầu-cuối**: Loại bỏ hoàn toàn các thao tác click chuột thủ công, giảm thời gian provision hệ thống lớn từ nhiều giờ xuống chỉ còn vài phút.
- **Nhất quán môi trường**: Đảm bảo cấu hình giữa các môi trường Phát triển (Development), Kiểm thử (Staging) và Triển khai thực tế (Production) hoàn toàn đồng nhất, loại bỏ lỗi cấu hình sai lệch (configuration drift).
- **Quản lý phiên bản (Version Control)**: Dễ dàng lưu trữ mã nguồn hạ tầng trên Git để theo dõi lịch sử thay đổi, thực hiện review code và khôi phục nhanh chóng khi xảy ra sự cố.

---

## 2. Kiến trúc cốt lõi của Oracle Database@AWS

Để triển khai bằng Terraform, chúng ta cần nắm rõ các thành phần kiến trúc chính sẽ được khởi tạo bao gồm:

- **ODB Network**: Hạ tầng mạng chuyên dụng tạo kết nối private bảo mật và tốc độ cao giữa AWS và Oracle Cloud Infrastructure (OCI).
- **Oracle Exadata Infrastructure**: Hệ thống phần cứng Exadata vật lý được đặt ngay trong các Availability Zone (AZ) của AWS.
- **Exadata VM Cluster / Autonomous VM Cluster**: Cụm máy ảo phân tán chạy trên hạ tầng Exadata, nơi trực tiếp vận hành cơ sở dữ liệu Oracle của bạn.
- **ODB Peering Connection**: Kết nối ngang hàng private giúp kết nối VPC chứa ứng dụng của bạn (EC2, EKS...) trực tiếp với ODB Network để truy vấn dữ liệu với độ trễ tối thiểu.

---

## 3. Điều kiện tiên quyết trước khi triển khai (Prerequisites)

Để mã nguồn Terraform có thể thực thi mượt mà, bạn cần đảm bảo hoàn tất các bước chuẩn bị sau:

- **Quy trình Onboarding**: Liên hệ phía Oracle để nhận Private Offer cho dịch vụ ODB@AWS thông qua AWS Marketplace.
- **Liên kết tài khoản**: Thực hiện liên kết thành công tài khoản AWS (AWS Account) với phân vùng tài nguyên Oracle (OCI Tenancy).
- **Cấu hình Provider**: Cấu hình đầy đủ thông tin xác thực cho cả AWS Provider và OCI Provider trong mã nguồn Terraform để có quyền can thiệp vào tài nguyên của cả hai nền tảng.

---

## 4. Quy trình triển khai bằng Terraform (Tóm tắt các bước)

Hạ tầng sẽ được khởi tạo tự động theo đúng trình tự phụ thuộc của các tài nguyên thông qua các khối mã (Resource Block) chuyên dụng:

**Bước 1: Khởi tạo ODB Network**

Tạo phân vùng mạng an toàn kết nối giữa AWS và OCI:

```terraform
resource "aws_oracle_odb_network" "example" {
  # Cấu hình dải IP (CIDR Block) và vị trí Availability Zone tương ứng
}
```

**Bước 2: Triển khai Hạ tầng Exadata**

Cấu hình phần cứng Exadata chuyên dụng nằm trong data center AWS:

```terraform
resource "aws_oracle_odb_cloud_exadata_infrastructure" "example" {
  # Định nghĩa quy mô phần cứng và liên kết với ODB Network vừa tạo
}
```

**Bước 3: Khởi tạo Exadata VM Cluster**

Tạo môi trường ảo hóa để chuẩn bị cài đặt cấu hình Database:

```terraform
resource "aws_oracle_odb_cloud_vm_cluster" "example" {
  # Cấu hình số lượng CPU Core, dung lượng Memory và Grid Infrastructure
}
```

**Bước 4: Thiết lập kết nối ODB Peering**

Mở đường truyền private cho phép ứng dụng từ VPC AWS truy cập thẳng vào database:

```terraform
resource "aws_oracle_odb_peering_connection" "example" {
  # Kết nối VPC chứa ứng dụng hiện tại với hạ tầng ODB vừa thiết lập
}
```

---

## 5. Đối tượng phù hợp với giải pháp này

- **Database Administrator (DBA)**: Các chuyên gia dữ liệu muốn nâng cao năng lực quản trị, dịch chuyển từ vận hành thủ công sang tư duy quản lý hạ tầng hiện đại.
- **DevOps / Cloud Engineer**: Những người chịu trách nhiệm tự động hóa luồng CI/CD cho hạ tầng, mong muốn quản lý Oracle Database đồng bộ như mọi tài nguyên Cloud khác.
- **Doanh nghiệp Enterprise**: Các tổ chức đang có lộ trình dịch chuyển hệ thống lõi (Core workload) chạy Oracle từ On-premises lên AWS nhưng vẫn yêu cầu khắt khe về hiệu năng đỉnh cao của Exadata.

---

## Kết luận

Ứng dụng Terraform để provision Oracle Database@AWS không chỉ giúp tăng tốc độ triển khai dự án mà còn tối ưu hóa chi phí vận hành, giảm thiểu tối đa rủi ro cấu hình sai do con người gây ra. Đây là một bước đi chiến lược và chuyên nghiệp cho bất kỳ tổ chức nào muốn khai thác trọn vẹn sức mạnh tính toán của Oracle Exadata cùng sự linh hoạt của hệ sinh thái đám mây AWS.

Nguồn: AWS Database Blog - Provision Oracle Database@AWS resources using Terraform.
