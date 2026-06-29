# 1. Dynamic scaling policies

- Target tracking scaling
- Simple/step scaling
- Schedule action
- Predictive scaling (ML need data historical at least 2 weeks)
  Note: Good metric for scale on:
  CPUUtilization, RequestCountPerTarget, Average Network In/Out, Custom metric (using push alarm metric)

# 2. Autoscaling good to know

- Spot fleet support
- Lifecycle hooks: before an instance is in service, or before it is terminated
  Apply: cleanup, log extraction, special health check


✅ Warmup Instance:

- Instance cần thời gian start app (5-10 phút)
- Mount vào DB RDS
- Bind secondary ENI

✅ Backup Data:

- Backup data trước terminate
- Copy logs lên S3
- Backup database snapshot

✅ Wait Request:

- Wait request đang xử lý finish
- Wait batch job finish
- Wait queue processing empty

✅ Attach Infrastructure:

- Attach vào CLB
- Mount vào ApsaraDB RDS
- Bind secondary ENI

✅ Custom Health Check:

- Verify app health (HTTP 200)
- Verify database connection

# 3. Upgrade AMI

- Update launch template/ launch configuration
- Terminate instance manually (cloudformation can help)
- Or use ec2 instance refresh for auto scaling

# 4. Scaling processes

- Launch
- Terminate
- HealthCheck
- ReplaceUnhealthy
- AZRebalance
- AlarmNotification
- ScheduledAction
- AddToLoadBalancer
- InstanceRefresh
