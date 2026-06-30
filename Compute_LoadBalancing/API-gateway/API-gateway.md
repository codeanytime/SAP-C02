# 1. API gateway overview

- Authorization
- versioning
- traffic management
- Serverless
- OpenAPI spec
- LIMIT: 29 second timeout
- LIMIT: 10MB request body (solution: use lambda), 32 MB response body

# 2. Deployment stage

state: dev, test, prod

# 3. API gateway integration

- HTTP
- Lambda function
- AWS service: step function

# 4. API gateway security

- Load SSL certificate
- Resource policy
- IAM execution role for API gateway

# 5. API gateway authentication

- IAM base access
- lambda authorizer
- Cognito User Pools

# 6. Logging, monitoring, tracing

- Cloudwatch log (enable at stage level)
- Can send log directly to Kinesis Data Firehose
- Cloudwatch metrics
- X-Ray
