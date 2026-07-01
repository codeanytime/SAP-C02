- EC2 on it owns EIP
- EC2 with route53
- ALB & ASG
- ALB with ECS on EC2
- ALB with ECS fargate
- ALB + Lambda
- API gateway + Lambda
- API gateway + aws service
- API gateway + HTTP backend (ex ALB)


## 1. EC2 on its own with EIP

* **Ưu điểm**
  * Đơn giản nhất: 1 EC2 + EIP, NAT ra/vào trực tiếp.
  * Không cần DNS, chỉ cần IP (hoặc sau này gắn vào Route53).
  * Quản lý full control OS, network.
* **Nhược điểm**
  * Không có HA: EC2 chết là downtime.
  * Tự lo scaling, rolling deploy, health check.
* **Use case:**
  * Lab, demo, môi trường dev cá nhân, hệ thống nội bộ không yêu cầu HA cao.


## 2. EC2 với Route53

* Route53 thực chất chỉ add **DNS layer + health check** phía trước EC2/ALB.
* **Ưu điểm:**
  * Có domain đẹp, dễ thay backend (thay IP/ALB mà không đổi client).
  * Có thể cấu hình health check, failover (VD: 2 EC2 ở 2 AZ/Region).[serverlessland](https://serverlessland.com/patterns/route53-alb-fargate-cdk-dotnet)
* **Nhược điểm:**
  * Nếu sau Route53 vẫn chỉ 1 EC2 thì HA vẫn thấp.
* **Use case:**
  * App nhỏ nhưng cần domain, SSL (thường đi kèm ACM + ALB sau này).

## 3. ALB & ASG (EC2)

* **Kiến trúc chuẩn web truyền thống:**
  * ALB (L7) nhận traffic HTTP/HTTPS, path‑based routing.
  * Sau ALB là **Auto Scaling Group** nhiều EC2.
* **Ưu điểm:**
  * HA multi‑AZ, scale theo CPU, RequestCount…
  * Hỗ trợ HTTP/2, WebSocket, sticky session, WAF, ACM TLS.
  * Phù hợp monolith Java/Spring Boot, .NET, PHP.
* **Nhược:**
  * Phải quản lý EC2 (patch, AMI, capacity plan).
* **Use case:**
  * Ứng dụng backend hiện tại của bạn đang chạy trên EC2, muốn scale chuẩn AWS.

## 4. ALB với ECS on EC2

* **Mô hình:** EC2 cluster (ECS), ALB target group đăng ký **ECS task** (container).
* **Ưu điểm:**
  * Dùng được benefit container: packaging, rollout theo task.
  * Có thể tận dụng EC2 Spot để giảm chi phí.**dev**+1
* **Nhược:**
  * Quản lý **2 lớp scaling**: EC2 + ECS service (số task).
  * Phức tạp hơn Fargate (capacity, bin packing, Daemon task…).
* **Use case:**
  * Workload container hóa, chạy liên tục, traffic ổn định; ưu tiên tối ưu chi phí hơn là tối giản vận hành.

## 5. ALB với ECS Fargate

* **Mô hình:** Không có EC2, mỗi task Fargate là 1 container serverless; ALB route đến task.[dev](https://dev.to/parag477/ecs-vs-eks-vs-lambda-how-to-pick-the-right-aws-compute-service-2026-24pg)
* **Ưu điểm:**
  * Không quản lý server; chỉ khai báo CPU/memory cho task.
  * Scale theo số task, dễ deploy blue/green, rolling.
* **Nhược:**
  * Cost cao hơn ECS on EC2 cho workload chạy 24/7 với utilization cao (Fargate giá /vCPU/hour cao).[dev](https://dev.to/parag477/ecs-vs-eks-vs-lambda-how-to-pick-the-right-aws-compute-service-2026-24pg)
* **Use case:**
  * Microservice, API, event‑driven, hoặc team nhỏ không muốn quản EC2, chấp nhận trade‑off chi phí.

## 6. ALB + Lambda

* ALB target type = Lambda: mỗi request HTTP → Lambda function.[cloudmentor](https://blog.cloudmentor.pro/posts/lambda-ecs-fargate-eks-va-ec2-so-sanh-toan-dien-de-chon-dung-compute-service-tren-aws)
* **Ưu điểm:**
  * Dùng khi cần L7 LB phức tạp (path‑based nhiều backend: ECS, Lambda, EC2) nhưng một số route muốn là Lambda.
  * Có thể keep ALB cho app hiện có (ECS/EC2) và thêm vài route serverless mà không cần API GW.
* **Nhược:**
  * Tốn chi phí ALB 24/7 + Lambda theo request → không tối ưu nếu chỉ có vài route.
* **Use case:**
  * Hệ thống chính đang dùng ALB, cần bổ sung thêm 1 vài endpoint Lambda (batch, webhook, converter) mà không muốn thêm API Gateway.

## 7. API Gateway + Lambda

* Đây là **serverless API pattern chuẩn**.**cloudmentor**+1
  * API Gateway làm HTTP front: routing, auth (JWT, Cognito, Lambda authorizer), throttling, usage plan.
  * Lambda xử lý business logic.
* **Ưu điểm:**
  * Không phải quản lý server; scale theo request.
  * Thích hợp cho **event‑driven**, traffic không đều (cao điểm / idle).
* **Nhược:**
  * **Cold start** (nhất là với runtime Java) nếu không tối ưu.
  * Limit: 15 phút / invocation; không phù hợp job lâu.[reddit](https://www.reddit.com/r/aws/comments/vb9k5z/lambda_vs_ecsfargate_when_deploying_an_api/)
* **Use case:**
  * Public API, webhook, backend cho SPA/mobile, microservice nhỏ, POC nhanh.

## 8. API Gateway + AWS service (service proxy)

* API Gateway tích hợp trực tiếp với S3, DynamoDB, Step Functions, Kinesis, SQS… (service integration).[aws.amazon](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-private-integration.html)
* **Ưu điểm:**
  * Xây REST API mà **không cần Lambda / ECS / EC2**.
  * Ít thành phần, latency tốt (API GW → service).[alexdebrie](https://alexdebrie.com/posts/aws-api-performance-comparison)
  * Rất rẻ, dễ vận hành.
* **Nhược:**
  * Logic phức tạp khó thể hiện chỉ bằng mapping template / Step Functions.
* **Use case:**
  * CRUD đơn giản với DynamoDB, upload/download S3, trigger workflow Step Functions, mà không cần nhiều logic.

## 9. API Gateway + HTTP backend (ALB, ECS, on‑prem…)

* API GW HTTP integration → (nếu private) VPC Link → ALB/NLB/ECS/EKS/EC2.**viblo**+1
* **Ưu điểm:**
  * Reuse backend sẵn có (ALB/ECS/EKS/EC2) nhưng thêm được **feature API GW**:
    * Auth (Cognito JWT, custom authorizer)
    * Throttling, usage plans, API key
    * Tách internal endpoint với public endpoint
* **Nhược:**
  * Thêm hop (API GW → ALB → backend) → tăng latency chút ít.[alexdebrie](https://alexdebrie.com/posts/aws-api-performance-comparison)
  * Phải quản 2 lớp config (API GW và ALB/backend).
* **Use case:**
  * Bạn đã có microservice stack trên ALB (ECS/EC2), muốn xuất ra public API có rate‑limit, multi‑tenant, API key billing.
