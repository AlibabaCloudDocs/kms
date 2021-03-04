# Key Store服务关联角色

本文为您介绍Key Store服务关联角色（AliyunServiceRoleForKMSKeyStore）的应用场景、权限策略、创建及删除操作。

## 应用场景

创建和使用Private Key Store中的用户主密钥时，密钥管理需要通过服务关联角色访问您的加密服务（Alibaba Cloud Data Encryption Service）。

关于服务关联角色的更多信息，请参见[服务关联角色](/intl.zh-CN/角色管理/服务关联角色.md)。

## 权限说明

角色名称：AliyunServiceRoleForKMSKeyStore。

权限策略：AliyunServiceRolePolicyForKMSKeyStore。

权限说明：密钥管理服务使用此角色访问您的加密服务、云服务器ECS、专有网络VPC等其他云服务资源。

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

## 创建服务关联角色

当您使用阿里云账号在密钥管理控制台首次创建Private Key Store时，会自动创建服务关联角色（AliyunServiceRoleForKMSKeyStore）。

当您使用的是RAM用户，需要先授权以下自定义策略，才能在密钥管理控制台首次创建Private Key Store时，自动创建服务关联角色（AliyunServiceRoleForKMSKeyStore）。具体操作，请参见[为RAM用户授权](/intl.zh-CN/用户管理/为RAM用户授权.md)。

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

## 删除服务关联角色

删除服务关联角色前，您需要在密钥管理控制台删除当前阿里云账号下的Private Key Store。具体操作，请参见[删除Private Key Store](/intl.zh-CN/密钥服务/Key Store/删除Private Key Store.md)。

您可以在RAM控制台删除服务关联角色。具体操作，请参见[删除RAM角色](/intl.zh-CN/角色管理/删除RAM角色.md)。

