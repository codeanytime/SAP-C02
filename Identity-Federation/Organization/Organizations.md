Organizations:

- Management account
- Member account
- OU: Group account (Dev, Prod, Test,..)

Restrict access: SCP (Apply in OU), SCP not apply in management account.
SCP often use deny list strategy.

Note:

- Organizations: Manage multiple account
- OU: group account
- SCP: Role apply for group account (OU)
- IAM policy: role detail on each account.
- Implicit deny: if not allow -> implicit deny (in allow list strategy)
