1. S3 access points: Endpoint tùy chỉnh gắn vào bucket để chia sẻ dữ liệu với nhiều ứng dụng/teams
2. S3 access points vs S3 vpc endpoint:
- S3 vpc endpoints: gateway endpoint va interface endpoint <-> Cach routing s3 va VPC
- S3 access points: share data beetween multiple apps, multiple team..
3. S3 object lambda access point: 

Use lambda function to change object before it is retrieve by caller application
- Use case: Mask PII.
- Convert data format (Ex: XML to Json)
- Resize and watermark image store in s3.

4. Compare between S3 access points vs S3 endpoint (Interface + gateway endpoint)
- Access point ban chat tao cong rieng vao cung 1 bucket. Moi app co yeu cau khac nhau va prefix trong cung bucket khac nhau.
- gateway endpoint: Giai quyet bai toan network cho S3 trong VPC. Cho phep EC2, lambda truy cap S3 ma khong
can NAT gateway, internet gateway. Tang tinh security.
Rieng doi voi gateway endpoint khong phat sinh chi phi, khong qua internet.