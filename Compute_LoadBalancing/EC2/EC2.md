1. Type:
- R: Ram
- C: CPU (compute/database)
- M: general/webapp
- I: IO (database)
- G: GPU video rendering/machine learning
- T2/T3: burtable instance, unlimited burst (2 mode)
2. EC2 placement group:
- Cluster: low latency group in 1 AZ
- Partition (Cassandra, kafka)
- Spread
3. EC2 instance launch type
- On demand
- Spot
- Reserved (minimum 1 year)
- Dedicated instance: book physical server