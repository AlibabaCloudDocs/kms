# 从ECS实例安全访问KMS

您可以为云服务器ECS创建RAM服务角色，使ECS实例内的应用程序可以使用STS临时凭证或者通过SDK访问KMS。

## 步骤一：创建实例RAM角色并授权

1.  创建实例RAM角色。

    在OpenAPI开发者门户中调用RAM的[CreateRole](https://next.api.aliyun.com/api/Ram/2015-05-01/CreateRole)接口，创建实例RAM角色（EcsRamRoleTest）。请求参数设置如下：

    -   RoleName：填写实例RAM角色名称（EcsRamRoleTest）。
    -   AssumeRolePolicyDocument： 填写如下策略内容，表示允许ECS扮演该角色。

        ```
        {
            "Statement": [
                {
                    "Action": "sts:AssumeRole", 
                    "Effect": "Allow", 
                    "Principal": {
                        "Service": [
                            "ecs.aliyuncs.com"
                        ]
                    }
                }
            ], 
            "Version": "1"
        }
        ```

2.  授予实例RAM角色访问KMS的权限。

    在OpenAPI开发者门户中调用RAM的[AttachPolicyToRole](https://next.api.aliyun.com/api/Ram/2015-05-01/AttachPolicyToRole)接口，为实例RAM角色（EcsRamRoleTest）添加AliyunKMSFullAccess系统权限。请求参数设置如下：

    -   PolicyType：填写System，表示系统策略。
    -   PolicyName：填写KMS系统策略名称（AliyunKMSFullAccess）。
    -   RoleName：填写实例RAM角色名称（EcsRamRoleTest）。

## 步骤二：授予实例RAM角色

您可以通过如下两种方式为ECS实例授予RAM角色：

-   为已有ECS实例授予实例RAM角色

    在OpenAPI开发者门户中调用ECS的[AttachInstanceRamRole](https://next.api.aliyun.com/api/Ecs/2014-05-26/AttachInstanceRamRole)接口，为已有的VPC类型ECS实例授予实例RAM角色。请求参数设置如下：

    -   RegionId：选择实例所在的地域ID。
    -   RamRoleName：填写实例RAM角色名称（EcsRamRoleTest）。
    -   InstanceIds：填写VPC类型ECS实例ID（\["i-bXXXXXXXX"\]）。
-   创建ECS实例时指定实例RAM角色
    1.  创建实例。

        在OpenAPI开发者门户中调用ECS的[CreateInstance](https://next.api.aliyun.com/api/Ecs/2014-05-26/CreateInstance)接口，创建ECS实例。请求参数设置如下：

        -   RegionId：选择实例所在地域（cn-hangzhou）。
        -   ImageId：填写实例的镜像（centos\_7\_03\_64\_40G\_alibase\_20170503.vhd）。
        -   InstanceType：填写实例的规格（ecs.g6.large）。
        -   VSwitchId：填写实例所在的VPC交换机。

            **说明：** 实例RAM角色目前只支持VPC类型ECS实例，该参数必填。

        -   RamRoleName：填写实例RAM角色名称（EcsRamRoleTest）。
        您也可以授权RAM用户使用实例RAM角色。具体操作，请参见[授权RAM用户使用实例RAM角色](/intl.zh-CN/安全/实例RAM角色/通过API使用实例RAM角色.md)。

    2.  设置密码并启动实例。
    3.  使用API或在控制台设置ECS实例访问公网的权限。

## 步骤三（可选）：获取临时授权Token

您可以获得实例RAM角色的临时授权Token，该临时授权Token可以执行实例RAM角色的权限和资源，并且自动周期性地更新。操作步骤如下：

1.  检索名为EcsRamRoleTest的实例RAM角色的临时授权Token。

    -   Linux实例：执行命令`http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest`。
    -   Windows实例：具体操作，请参见[实例元数据](/intl.zh-CN/实例/管理实例/使用实例元数据/ECS实例元数据概述.md)。
2.  获得临时授权Token。

    返回示例如下：

    ```
    {
       "AccessKeyId" : "STS.J8XXXXXXXXXX4",
       "AccessKeySecret" : "9PjfXXXXXXXXXBf2XAW",
       "Expiration" : "2017-06-09T09:17:19Z",
       "SecurityToken" : "CAIXXXXXXXXXXXwmBkleCTkyI+",
       "LastUpdated" : "2017-06-09T03:17:18Z",
       "Code" : "Success"
    }
    ```


## 步骤四：使用SDK访问KMS

通过如下三种方式使用SDK访问KMS：



