1. AWS Shield: DDOS protect
- Dịch vụ bảo vệ DDoS cho các resource public như CloudFront, ALB, API Gateway, Route 53, Global Accelerator, EC2.
- Shield Standard: bật mặc định, miễn phí, bảo vệ L3–L4 cơ bản.
- Shield Advanced: trả phí, thêm detection/mitigation nâng cao, nhiều dịch vụ được hỗ trợ, metrics, DDoS cost protection, và tích hợp sâu với WAF để bảo vệ L7.
- Pham vi resource: CloudFront, ALB/NLB, Route 53, Global Accelerator, một số EC2, API Gateway (với Advanced)
2. AWS WAF (Web Application Firewall)
- Firewall cho ứng dụng web/API ở Layer 7 (HTTP/HTTPS).
- Cho phép define rule để allow/block/count request theo IP, country, pattern trong URL/header/body, SQLi/XSS, rate limiting, JA3/JA4 fingerprint, v.v.
- Gắn được vào CloudFront, ALB, API Gateway, AppSync, Cognito, Verified Access, v.v.
- Pham vi resource: CloudFront, ALB, API Gateway, AppSync, Cognito, Verified Access, v.v.
3. AWS Firewall Manager:
- Công cụ quản lý tập trung WAF, Shield Advanced, Network Firewall, security group, Route 53 Resolver DNS Firewall… trên nhiều account/resources trong một AWS Organization.
- Bạn define policy một lần (ví dụ “mọi CloudFront phải có WAF X”) và Firewall Manager tự apply/enforce khi có account hoặc resource mới.
- Pham vi resource: WAF, Shield Advanced, Network Firewall, VPC SG, Route 53 Resolver DNS Firewall trên toàn Org.
4. Inspector: tìm lỗ hổng trong EC2/container/Lambda/mã nguồn (thiên về vulnerability management).
