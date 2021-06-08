# 动态ECS凭据服务关联角色

当您使用KMS的动态ECS凭据功能时，需要通过服务关联角色授予凭据管家访问ECS、云助手等相关资源的权限。本文为您介绍动态ECS凭据服务关联角色（AliyunServiceRoleForKMSSecretsManagerForECS）的权限策略、创建及删除操作。

## 权限说明

角色名称：AliyunServiceRoleForKMSSecretsManagerForECS

权限策略：AliyunServiceRolePolicyForKMSSecretsManagerForECS

权限说明：凭据管家使用该角色为您管理动态ECS凭据，完成ECS口令、公私钥的轮转任务。

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

## 创建服务关联角色

在创建动态ECS凭据的过程中，如果之前没有创建过服务关联角色，会自动进行创建。

## 删除服务关联角色

删除服务关联角色前，您需要先删除当前阿里云账号下的动态ECS凭据，然后在RAM控制台删除服务关联角色。具体操作，请参见[删除RAM角色](/cn.zh-CN/角色管理/删除RAM角色.md)。

