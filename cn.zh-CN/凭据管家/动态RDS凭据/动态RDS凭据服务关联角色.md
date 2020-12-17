# 动态RDS凭据服务关联角色

当您使用KMS的动态RDS凭据功能时，需要通过服务服务关联角色，访问阿里云关系型数据库RDS（Relational Database Service）相关资源。本文为您介绍动态RDS凭据服务关联角色（AliyunServiceRoleForKMSSecretsManagerForRDS）的权限策略、创建及删除操作。

## 权限说明

角色名称：AliyunServiceRoleForKMSSecretsManagerForRDS。

权限策略：AliyunServiceRolePolicyForKMSSecretsManagerForRDS。

权限说明：凭据管家使用该角色为您管理动态RDS凭据，完成RDS账号口令的轮转等任务。

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

## 创建服务关联角色

在创建动态RDS凭据的过程中，如果之前没有创建过服务关联角色，会自动进行创建。

## 删除服务关联角色

删除服务关联角色前，您需要先删除当前阿里云账号下的动态RDS凭据，然后在RAM控制台删除服务关联角色。具体操作，请参见[删除RAM角色](/cn.zh-CN/角色管理/删除RAM角色.md)。

