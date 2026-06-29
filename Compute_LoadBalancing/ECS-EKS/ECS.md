# 1. Docker container management on AWS

- ECS
- EKS
- Fargate: serverless, work with ECS and EKS

# 2. ECS

- Use case:
  - Run microservice
  - Run batch processing/ schedule task
  - Migrate application to cloud
- Concept:
  - Cluster: logical grouping of EC2 instance
  - Service: define how many task should run and how they should be run
  - Task definition: metadata how to run docker container (image name, CPU, ..)
  - ECS task: an instance of task definition, a running docker container
  - ECS IAM role

# 3. ECS vs ALB integration

Dynamic port mapping voi truong hop Ec2. Fargate khong can care port conflict.

# 4.ECS security & networking

- None: khong can giao tiep ben ngoai, app doc lap, ML.
- bridge: dung mang docker (dynamic port mapping voi type ec2)
- host: workload can latency cuc thap, tuy nhien khong chay duoc 2 task/loai tren cung 1 ec2 do conflict port.
- awsvpc: fargate (bat buoc)

# 5. ECS - spot instance

- ECS classic (EC2 type): Good for cost saving but may impact reliability
- Fargate: Specify minimum of task for on-demand baseline workload, can use FARGATE_SPOT for cost saving

# 6. ECR

Container registry

- Access is controlled through IAM
- Support image scanning, vulnerability scanning, image lifecycle, image tag..
