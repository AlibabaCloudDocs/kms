# Manage the service-linked role for dynamic ECS secrets

To use dynamic Elastic Compute Service \(ECS\) secrets in Key Management Service \(KMS\), you must use a service-linked role to grant Secrets Manager the permissions to access related resources, such as ECS instances and Cloud Assistant. This topic describes the permission policy of the service-linked role AliyunServiceRoleForKMSSecretsManagerForECS for dynamic ECS secrets and how to create and delete the role.

## Permission description

Role name: AliyunServiceRoleForKMSSecretsManagerForECS.

Policy: AliyunServiceRolePolicyForKMSSecretsManagerForECS.

Permission description: Secrets Manager uses this role to manage dynamic ECS secrets. For example, Secrets Manager uses this role to rotate passwords and SSH keys for ECS instances.

```
{
  "Version": "1",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ecs:DescribeInstances",
        "ecs:InvokeCommand",
        "ecs:DescribeInvocationResults"
      ],
      "Resource": [
        "acs:ecs:*:*:instance/*",
        "acs:ecs:*:*:command/cmd-ACS-KMS-RotateECSSecret*"
      ]
    },
    {
      "Action": [
        "kms:ListSecretVersionIds",
        "kms:GetSecretValue",
        "kms:DescribeSecret",
        "kms:PutSecretValue",
        "kms:UpdateSecretVersionStage"
      ],
      "Resource": "acs:kms:*:*:secret/acs/ecs/*",
      "Effect": "Allow"
    },
    {
      "Action": "ram:DeleteServiceLinkedRole",
      "Resource": "*",
      "Effect": "Allow",
      "Condition": {
        "StringEquals": {
          "ram:ServiceName": "secretsmanager-ecs.kms.aliyuncs.com"
        }
      }
    }
  ]
}
```

## Create the service-linked role

If the service-linked role has not been created, it is automatically created when you create a dynamic ECS secret.

## Delete the service-linked role

Before you delete the service-linked role, you must delete the dynamic ECS secrets of the current Alibaba Cloud account. Then, you can delete the service-linked role in the RAM console. For more information, see [Delete a RAM role](/intl.en-US/RAM Role Management/Delete a RAM role.md).

