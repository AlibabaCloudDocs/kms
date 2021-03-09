# Service-linked role for key stores

This topic describes the scenarios and policies of the service-linked role AliyunServiceRoleForKMSKeyStore for key stores. This topic also shows you how to create and delete the AliyunServiceRoleForKMSKeyStore role.

## Scenarios

If you want to create and use a customer master key \(CMK\) in a private key store, Key Management Service \(KMS\) must access your Alibaba Cloud Data Encryption Service by using a service-linked role.

For more information about service-linked roles, see [Service-linked roles](/intl.en-US/RAM Role Management/Service-linked roles.md).

## Permission description

Role name: AliyunServiceRoleForKMSKeyStore.

Policy name of the role: AliyunServiceRolePolicyForKMSKeyStore.

Permission description: KMS uses this role to access resources of other Alibaba Cloud services such as Data Encryption Service, Elastic Compute Service \(ECS\), and Virtual Private Cloud \(VPC\).

```
{
  "Version": "1",
  "Statement": [
    {
      "Action": [
        "ecs:CreateNetworkInterfacePermission",
        "ecs:DeleteNetworkInterfacePermission",
        "ecs:CreateNetworkInterface",
        "ecs:DescribeNetworkInterfaces",
        "ecs:DescribeSecurityGroups",
        "ecs:CreateSecurityGroup",
        "ecs:DeleteSecurityGroup",
        "ecs:AuthorizeSecurityGroup",
        "ecs:AuthorizeSecurityGroupEgress",
        "ecs:RevokeSecurityGroup",
        "ecs:RevokeSecurityGroupEgress",
        "ecs:DescribeSecurityGroupAttribute"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "vpc:DescribeVSwitches",
        "vpc:DescribeVpcs"
      ],
      "Resource": "*",
      "Effect": "Allow"
    },
    {
      "Action": [
        "yundun-hsm:DescribeInstances",
        "yundun-hsm:DescribeClusters"
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
          "ram:ServiceName": "keystore.kms.aliyuncs.com"
        }
      }
    }
  ]
}
```

## Create the service-linked role AliyunServiceRoleForKMSKeyStore

When you create a private key store in the KMS console for the first time by using an Alibaba Cloud account, the service-linked role AliyunServiceRoleForKMSKeyStore is automatically created.

If you are using a RAM user, the following custom policy must be attached to the RAM user. Then, the service-linked role AliyunServiceRoleForKMSKeyStore is automatically created when you create a private key store in the KMS console for the first time. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md).

```
{
    "Action": "ram:CreateServiceLinkedRole",
    "Resource": "*",
    "Effect": "Allow",
    "Condition": {
        "StringEquals": {
            "ram:ServiceName": "keystore.kms.aliyuncs.com"
        }
     }
}
```

## Delete the service-linked role AliyunServiceRoleForKMSKeyStore

Before you delete the service-linked role AliyunServiceRoleForKMSKeyStore, you must delete the private key stores within the current Alibaba Cloud account in the KMS console. For more information, see [Delete a private key store](/intl.en-US/Key Service/Key Store/Delete a private key store.md).

You can delete the service-linked role AliyunServiceRoleForKMSKeyStore in the RAM console. For more information, see [Delete a RAM role](/intl.en-US/RAM Role Management/Delete a RAM role.md).

