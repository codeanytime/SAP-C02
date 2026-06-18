1. KMS (IAM)

   regional service but support multi regional

    3 type
   - Customer managed key
   - AWS managed key
   - AWS Owned key

    Note: Key material: use for encrypt and decrypt (cannot be change after creation)
    3 type key material:
    - AWS_KMS
    - EXTERNAL
    - CLOUDHSM
    - EXTERNAL_KEY_STORE

2. SSM parameter store (IAM)
    
    Parameter store hierarchy, TTL (expire if setting)

    Limit: 4kb value (standard free), 8kb value (advance no free)

3. Secrets manager

Note: 

    So sanh 3 dich vu
    KMS support cross-account
    Parameter store not support cross-account (phuc tap phai thong qua assume role)
    Secret manager support cross-account

    SSM Parameter store khong support resource base policy

    


