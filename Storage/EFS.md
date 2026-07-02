# 1. EFS

- Network file system can be mounted on many EC2
- Multi AZ
- Serveless
- HA, scalable, expensive (3x gp2), pay per GB use
- Use NFSv4.1 protocol

# 2. Use case

- Content management
- Web serving
- Data sharing
- Wordpress
- Compatible with Linux AMI (not window), POSIX-compliant
- Use security group for control access
- Encryption using KMS
- File system scale automatically

# 3. Perf & Storage class

- EFS has 2 perf mode
  - General Purpose: latency thấp nhất
  - Max I/O (IOPS aggregate cao, latency cao hơn), không hỗ trợ elastic throughput (big data, media rendering, high parallel)
- 3 throughput mode:
  - Elastic
  - Bursting: throughput tỉ lệ thuận dung lượng lưu trữ
  - Provisioned throughput: Không phụ thuộc dung lượng lưu trữ
- Lifecycle Management: EFS cho phép quản lý vòng đời.
  - EFS Standard     │ không truy cập N ngày → Transition into IA     ▼ EFS Infrequent Access (IA)     │ không truy cập M ngày → Transition into Archive     ▼ EFS Archive     │ được truy cập → Transition back to Standard (nếu bật)
