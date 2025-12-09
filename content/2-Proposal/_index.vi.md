---
title: "Đề Xuất"
date: 2025-10-11
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Dự Án AWS Security Scan – Kế Hoạch Dự Án  
## [Team DevSecOps FCJ] – [Đại học FPT / Chương trình Thực tập] – [Dự Án AWS Security Scan]
Date: 2025-10-11

### MỤC LỤC
1. NỀN TẢNG VÀ ĐỘNG LỰC  

 1.1 TÓM TẮT ĐIỀU HÀNH

 1.2 TIÊU CHÍ THÀNH CÔNG CỦA DỰ ÁN

 1.3 CÁC GIẢ ĐỊNH


2. KIẾN TRÚC GIẢI PHÁP / SƠ ĐỒ KIẾN TRÚC

 2.1 SƠ ĐỒ KIẾN TRÚC KỸ THUẬT

 2.2 KẾ HOẠCH KỸ THUẬT

 2.3 KẾ HOẠCH DỰ ÁN

 2.4 CÁC LƯU Ý BẢO MẬT



3. HOẠT ĐỘNG VÀ SẢN PHẨM BÀN GIAO

 3.1 HOẠT ĐỘNG VÀ SẢN PHẨM BÀN GIAO

 3.2 PHẠM VI LOẠI TRỪ

 3.3 LỘ TRÌNH LÊN PRODUCTION


4. DỰ TRÙ CHI PHÍ AWS THEO DỊCH VỤ

5. ĐỘI NGŨ

6. TÀI NGUYÊN & CHI PHÍ ƯỚC TÍNH

7. NGHIỆM THU



### 1. NỀN TẢNG VÀ ĐỘNG LỰC
### 1.1 TÓM TẮT ĐIỀU HÀNH  
Dự án AWS Security Scan nhằm tự động hóa quy trình kiểm tra bảo mật trên toàn bộ vòng đời phát triển phần mềm bằng cách tích hợp các dịch vụ AWS như CodePipeline, CodeBuild, CodeGuru Reviewer và AWS Security Hub.  
Sáng kiến này giúp tăng cường khả năng bảo mật của pipeline CI/CD bằng cách tích hợp quét lỗ hổng tự động, phân tích mã nguồn bằng AI và giám sát sự cố tập trung.

Các trường hợp sử dụng bao gồm:

- Tích hợp liên tục với xác thực bảo mật tích hợp sẵn  
- Cảnh báo tự động và báo cáo tuân thủ  
- Quan sát thời gian thực về lỗ hổng và chất lượng mã  

Dịch vụ của đối tác tập trung vào thiết kế, triển khai và tối ưu hóa pipeline DevSecOps, đảm bảo phân phối phần mềm an toàn, tuân thủ và hiệu quả.

### 1.2 TIÊU CHÍ THÀNH CÔNG CỦA DỰ ÁN  
- ≥95% các commit vượt qua quét bảo mật tự động trước khi triển khai  
- Cảnh báo thời gian thực trong vòng 2 phút khi phát hiện bất thường  
- Điểm tuân thủ Security Hub ≥90%  
- Tích hợp thành công giữa CodePipeline, CodeBuild và Security Hub mà không cần thao tác thủ công  

### 1.3 CÁC GIẢ ĐỊNH  
- Tất cả tài khoản AWS đã được cấu hình IAM phù hợp cho CodePipeline và CodeBuild  
- GitLab bật webhook và cấp quyền đầy đủ  
- Các công cụ bảo mật (Trivy, Bandit, SonarQube) sẵn sàng trong môi trường CodeBuild  
- Tổ chức tuân thủ AWS Well-Architected Framework và các best practice bảo mật  

### 2. KIẾN TRÚC GIẢI PHÁP / SƠ ĐỒ KIẾN TRÚC
### 2.1 SƠ ĐỒ KIẾN TRÚC KỸ THUẬT

Giải pháp đề xuất tích hợp nhiều dịch vụ AWS cho CI/CD, phân tích bảo mật tự động và giám sát.  
Bao gồm các thành phần: GitLab (source), CodeBuild (build/test), CodePipeline (orchestrator), CodeGuru Reviewer (AI code review), Security Hub + SNS (cảnh báo tập trung).

![Technical Architecture](/images/2-Proposal/architecture.png)

#### Công cụ sử dụng:
- GitLab  
- AWS CodePipeline  
- AWS CodeBuild  
- AWS CodeGuru Reviewer  
- AWS Security Hub, GuardDuty, Detective  
- SonarQube, Trivy, Bandit  

### 2.2 KẾ HOẠCH KỸ THUẬT

Đối tác sẽ xây dựng các file buildspec YAML cho CodeBuild để tự động:

- Quét mã nguồn (Trivy, Bandit)  
- Phân tích mã tĩnh (CodeGuru Reviewer)  
- Đóng gói và kích hoạt triển khai  

Tất cả triển khai được quản lý version qua GitLab CI triggers.  
Các file cấu hình tuân theo nguyên tắc Infrastructure as Code bằng AWS CloudFormation.

### 2.3 KẾ HOẠCH DỰ ÁN

Nhóm áp dụng Agile Scrum trong 4 sprint (mỗi sprint 2 tuần).  
Stakeholder tham gia Sprint Review và Retrospective.

Vai trò:

- DevOps Engineer: Thiết lập pipeline CI/CD  
- Security Engineer: Tích hợp và phân tích bảo mật  
- Project Lead: Điều phối, báo cáo, tài liệu  

Họp sync hàng tuần qua Slack và AWS Chime.

### 2.4 CÁC LƯU Ý BẢO MẬT

- Truy cập: IAM least privilege, MFA cho tài khoản admin  
- Hạ tầng: Subnet riêng tư cho build agents  
- Dữ liệu: Mã hóa S3 (SSE-KMS), mã hóa log CodeBuild  
- Giám sát: GuardDuty và Security Hub theo dõi liên tục  
- Quản lý sự cố: SNS + CloudWatch Alarms  

### 3. HOẠT ĐỘNG VÀ SẢN PHẨM BÀN GIAO
### 3.1 HOẠT ĐỘNG VÀ SẢN PHẨM BÀN GIAO

| Giai đoạn dự án          | Thời gian | Hoạt động                           | Sản phẩm / Mốc hoàn thành        | Man-days |
|--------------------------|-----------|--------------------------------------|----------------------------------|----------|
| Đánh giá                 | Tuần 1–2  | Phân tích CI/CD hiện tại             | Báo cáo & thiết kế kiến trúc     | 5        |
| Thiết lập hạ tầng cơ bản | Tuần 3–4  | Tạo CodePipeline & CodeBuild         | Pipeline triển khai hoàn chỉnh   | 7        |
| Tích hợp công cụ bảo mật | Tuần 5–6  | Thêm SonarQube, Trivy, Bandit        | Bật tính năng quét bảo mật       | 6        |
| Thiết lập giám sát       | Tuần 7    | Kết nối Security Hub, CloudWatch     | Hệ thống cảnh báo hoạt động      | 4        |
| Kiểm thử & Go-Live       | Tuần 8    | Kiểm thử cuối, tài liệu              | Báo cáo Go-Live                   | 3        |
| Bàn giao                 | Tuần 9    | Chuyển giao & hướng dẫn              | Tài liệu bàn giao cuối            | 2        |

### 3.2 PHẠM VI LOẠI TRỪ

- Quét bảo mật ứng dụng on-premises  
- Các framework tuân thủ không thuộc AWS  
- CI/CD ngoài AWS  

### 3.3 LỘ TRÌNH LÊN PRODUCTION

PoC tập trung vào tích hợp DevSecOps native trên AWS.  
Để đưa vào production, cần thêm các bước như multi-account, cô lập mạng, tự động vá lỗi.

### 4. DỰ TRÙ CHI PHÍ AWS THEO DỊCH VỤ

| Dịch vụ           | Mô tả                     | Ước tính chi phí/tháng (USD) |
|-------------------|---------------------------|-------------------------------|
| CodePipeline      | Orchestration             | 10                            |
| CodeBuild         | Build + Quét              | 30                            |
| CodeGuru Reviewer | Phân tích mã              | 25                            |
| Security Hub      | Tổng hợp + Cảnh báo       | 15                            |
| CloudWatch        | Logs + Metrics            | 10                            |
| S3                | Lưu artifact              | 5                             |
| SNS               | Thông báo                 | 5                             |
| **Tổng**          |                           | **100 USD/tháng**             |

### 5. ĐỘI NGŨ

| Tên               | MSSV      | Email / Liên hệ                     |
|------------------|-----------|--------------------------------------|
| Lê Công Cảnh     | SE183750  | canhlcse183750@fpt.edu.vn           |
| Phùng Gia Đức    | SE183187  | ducpgse183187@fpt.edu.vn            |
| Vũ Nguyễn Bình   | SE193185  | vunguyenbinh25@gmail.com            |
| Lê Minh Dương    | SE184079  | duonglmse184079@fpt.edu.vn          |
| Nguyễn Phi Duy   | SE180529  | duynpse180529@fpt.edu.vn            |

### 6. TÀI NGUYÊN & CHI PHÍ ƯỚC TÍNH

| Vai trò            | Trách nhiệm               | Rate (USD/hr) | Số giờ | Chi phí (USD) |
|--------------------|---------------------------|---------------|--------|----------------|
| Solution Architect | Thiết kế & rà soát        | 60            | 40     | 2400           |
| DevOps Engineer    | Triển khai pipeline       | 45            | 60     | 2700           |
| Security Engineer  | Tích hợp công cụ bảo mật  | 50            | 50     | 2500           |
| **Tổng**           |                           |               | 150    | **7600**       |

### 7. NGHIỆM THU

Sau mỗi giai đoạn, đối tác sẽ gửi sản phẩm bàn giao để khách hàng đánh giá.  
Khách hàng có 8 ngày làm việc để:

- Gửi chấp nhận bằng văn bản, hoặc  
- Gửi phản hồi từ chối cùng góp ý  

Nếu không phản hồi trong thời hạn, sản phẩm được xem như **được nghiệm thu**.

