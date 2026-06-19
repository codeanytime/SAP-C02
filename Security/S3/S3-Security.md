1. Encrypt for object
- SSE-S3
- SSE-KMS: On s3:PutObject, need kms:GenerateDataKey
- SSE-C
- Client side encryption
- Glacier: all data is AES-256 encrypted
2. Encrypt in transit (SSL/TLS)
- Http
- Https: aws:SecureTransport
3. Event in S3
- S3 access log
- S3 event notification: destination SQS, SNS, 
- Trust advisor
- Event bridge
4. S3 security
- IAM policy
- Resource base policy: ACL (bucket, object policy)
5. S3 presigned URL
6. VPC gateway endpoint for S3
7. Object lock & Glacier vault lock (WORM)

