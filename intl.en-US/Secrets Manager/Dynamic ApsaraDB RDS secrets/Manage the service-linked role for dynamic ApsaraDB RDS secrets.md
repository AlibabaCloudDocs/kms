# Manage the service-linked role for dynamic ApsaraDB RDS secrets

When you use the dynamic RDS secret feature, Key Management Service \(KMS\) must use a service-linked role to access the resources of ApsaraDB RDS. This topic describes the permission policy of the service-linked role AliyunServiceRoleForKMSSecretsManagerForRDS for dynamic ApsaraDB RDS secrets and how to create and delete the role.

## Permission description

Role name: AliyunServiceRoleForKMSSecretsManagerForRDS.

Policy: AliyunServiceRolePolicyForKMSSecretsManagerForRDS.

Permission description: Secrets Manager uses this role to perform tasks related to ApsaraDB RDS. For example, Secrets Manager uses this role to manage dynamic ApsaraDB RDS secrets and rotate the account passwords of ApsaraDB RDS instances.

```
{
  "Statement": [
    {
      "Action": [
        "rds:ResetAccountPassword",
        "rds:DescribeDBInstanceAttribute",
        "rds:DescribeAccounts"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": "ram:DeleteServiceLinkedRole",
      "Resource": "*",
      "Effect": "Allow",
      "Condition": {
        "StringEquals": {
          "ram:ServiceName": "secretsmanager-rds.kms.aliyuncs.com"
        }
      }
    }
  ],
  "Version": "1"
}
```

## Create the service-linked role

If the service-linked role has not been created, it is automatically created when you create a dynamic ApsaraDB RDS secret.

## Delete the service-linked role

Before you delete the service-linked role, you must delete the dynamic ApsaraDB RDS secrets of the current Alibaba Cloud account. Then, you can delete the service-linked role in the RAM console. For more information, see [Delete a RAM role](/intl.en-US/RAM Role Management/Delete a RAM role.md).

