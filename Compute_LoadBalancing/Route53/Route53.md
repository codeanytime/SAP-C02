# 1. Route 53 record type

- A: IP
- AAAA: maps host name to IPv6
- CNAME: host name to another hostname
  - Khong the tao ban ghi CNAME cho top node cua DNS namespace
  - VD: có thể tạo cho www.example.com nhưng không thể tạo cho example.com
- NS: name server for host zone

# 2. CNAME vs Alias

Nên dùng alias vì sẽ hoạt động cho cả root trong khi cname sẽ không work với root.


Alias free

# 3. Alias record type

- ELB
- Cloudfront
- API gateway
- Elastic beanstalk
- S3 website
- VPC interface endpoint
- Global accelerator
- Route53 record in the same hostzone
  Note: Không thể set alias cho EC2 DNS name.

# 4. Route53 TTL

Except alias record, TTL is mandatory for each DNS record.

# 5. Routing policy

- Simple
- Weighted
- Latency-based
- Failover: Active-passive (health check mandatory)
- Geolocation
- Geoproximity (Traffic flow)
- Multi value
- IP based

# 6. Route53 note

- For internal private DNS: must enable VPC setting: enableDNSHostnames + enableDnsSupport
- DNS security extension
