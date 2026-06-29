# 1. Spot Instance

EC2 instance sử dụng **tài nguyên dư thừa (unused capacity)** của AWS data center, được bán với giá rẻ hơn On-Demand tới **90%**.

# 2. Spot Fleet

Set of Spot instance + On-demand instance (optional)

Using Spot fleet request.

Spot fleet request:

- Target capacity: tổng dung lượng cần (Số instance, unit, vCPU)
- Mix spot/ ondemand
- Launch specification / launch template: type, AMI, AZ, SG
- Allocation strategy: Cách fleet chọn pool
  - lowestPrice: chi phí thấp nhất phù hợp short workload
  - diversified: distribute across all pools (great for availability, long workload)
  - capacityOptimized
  - priceCapacityOptimized (recommend): pools with highest capacity available, then select the pool lowest price (best choice for most workloads)
