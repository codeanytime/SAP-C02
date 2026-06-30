# 1. Lambda limit

- RAM: 128MB -> 10240MB
- CPU link RAM
- Timeout: 15 minutes
- /tmp storage: 10240MB
- Deployment package: 50MB (Zipped), 250MB (unzipped) including layers
- Concurrent executions: 1000
- Container image size: 10GB
- Invocation payload: 6MB sync, 256KB async

# 2. Lambda concurrency & throttling

- Concurrency limit: 1000 per region
  - EX: function A (100) -> available 900 (1000 - 100)
  - function A reserved 100, running 50 -> available 900 (1000 - 100 reserved)
- Reserved concurrency: Ensure capacity (guarantee min, max) (no fee addition)
  - Use case: Critical function (for ensure capacity)
- Provision concurrency: Reduce cold start, reduce latency
  - Use case: interactive workloads sensitive latency (web/mobile apps)
- Should use lambda in JS for reduce start time, use go/py for reduce execute time.
- If function limit (> 1000) -> 429 error -> request increase in service quota.
- How to estimate: Concurrency = (average requests per second) × (average request duration in seconds)
  - For critical: set >= peak (`CloudWatch metric: ConcurrentExecutions` check `average and peak concurrent requests`)

# 3. Lambda & CodeDeploy

CodeDeploy can help automate traffic shift for lambda

- Linear
- Canary
- AllAtOnce

Can create pre & post traffic hooks to check the health of the lambda function.

# 4. Logging, monitoring, tracing

- Cloudwatch
- XRay

# 5. Lambda in VPC

- Lambda in public subnet cannot access internet (lambda hasn't public ip)
  - Solution: move lambda to private subnet. use NAT gateway, internet gateway.
- Fix public ip for communication: use NAT gateway (EIP attach in NAT gateway)
