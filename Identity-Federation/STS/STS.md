STS Important API:

1. AssumeRole: access role within account or cross-account
2. AssumeRoleWithSAML: return credentials for users log with SAML
3. AssumRoleWithWebIdentity: return creds for user log with IDP
   Example: google, OpenId
   AWS recommends using cognito instead.
4. GetSessionToken: for MFA, from a user or AWS account root user
5. GetFederationToken: obtain temporary creds for a federated user

## Cách nhớ nhanh

* **AssumeRole**: “Tôi có AWS credentials, tôi muốn sang role khác.”
* **AssumeRoleWithSAML**: “Tôi đăng nhập qua SSO doanh nghiệp.”
* **AssumeRoleWithWebIdentity**: “Tôi đăng nhập qua Google/Facebook/Cognito.”
* **GetSessionToken**: “Tôi là IAM user, tôi muốn token tạm, thường kèm MFA.”
* **GetFederationToken**: “Tôi cần token tạm cho federated/external user.”
