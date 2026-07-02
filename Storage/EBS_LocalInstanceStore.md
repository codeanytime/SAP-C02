# 1. EBS

- Network drive attach only 1 instance (except using multi attach feature)
- Link to AZ (transfer: create snapshot -> restore)
- Volume can be resize

# 2. EBS volume type

- gp2/gp3: general purpose SSD balance price and perf
- io1/io2: highest perf SSD for mission critical low-latency or high throughput workload
- st1 (HDD): HDD, throughput-intensive workload, frequently access data
- sc1 (HDD): less frequently access workload, lowest cost HDD
- Phân loại theo kích thước, thông lượng, IOPS
  - Only gp2/gp3, io1/io2 can be use as boot volume

# 3. EBS snapshot

- Can copy snapshot across region
- Snapshot will store in s3 but you won't directly see them
- Not necessary to detach volume to do snapshot but recommend
- EBS backup use IO, if application handle lot of traffic shouldn't backup.
- Can make AMI from snapshot
- EBS volume restore by snapshot need to be pre-warmed (use Fast snapshot restore or use fio/dd command)

# 4. AWS Data Lifecycle Manager vs AWS Backup

> - Data lifecycle manager: automate create, retention, delete snapshot EBS
> - monitor and manage backup across the aws service you use
>   Difference about scope, ease of management

# 5. EBS encryption

- Account level setting apply per region
  - region A turn on, region B turn off -> all ebs in region A encrypt, region B encrypt or not.

# 6. EBS multi-attach

Only for io1/io2 family

- Attach same ebs volume for multi instance in same AZ
- Comparisons with EFS: multi-attach apply only in same AZ, lower latency than EFS (EFS need network share file), multi-attach mean share block level.

# 7. Local EC2 Instance Store

- Physical disk attach to the physical server where EC2 is
- Very high IOPs
- Block Storage (same EBS)
- cannot change size
- Good for buffer, cache, scratch data, temporary content
- Data lost if instance stop/terminate
