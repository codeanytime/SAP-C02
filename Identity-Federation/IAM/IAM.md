1. Users: long term credential
2. Groups: Tập hợp các IAM-user tạo thành nhóm.
   1 user có thể thuộc nhiều groups.
   Không có nested groups.
   Ví dụ: tạo các groups (developer, tester,..)
   1 user thuộc groups tự động có quyền thuộc groups đó.
3. Roles: short term credential, sử dụng STS
   Ec2 instance role
   Service role
   Cross-account-role
4. Policies: Policy định nghĩa action (allow/deny)
   AWS managed
   Customer managed
   Inlined policy
5. Resource base policy: SQS, S3 bucket, SNS, Lambda
   Hiểu trường hợp nào nên dùng Deny / NotAction
   Deny sẽ có mức độ ưu tiên cao nhất và ghi đè action allow.
6. Deepdive IAM role vs Resource base policy:
   IAM role: từ bỏ mọi quyền hiện tại của user, áp dụng quyền của IAM role
   Resource base policy: quyền của user vẫn còn.
7. IAM permission boundary
   Quyền tối đa áp dụng cho identity entity (cấp độ user/role)