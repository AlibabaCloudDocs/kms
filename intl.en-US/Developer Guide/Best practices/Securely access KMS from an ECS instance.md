# Securely access KMS from an ECS instance

You can create a RAM role for an Elastic Compute Service \(ECS\) instance. This way, applications on the ECS instance can access Key Management Service \(KMS\) by using a temporary Security Token Service \(STS\) credential and SDKs.

## Step 1: Create a RAM role and attach a permission policy to the role

1.  Create a RAM role.

    Use OpenAPI Explorer to call the [CreateRole](https://api.aliyun.com/#/?product=Ram&api=CreateRole) operation of RAM to create the RAM role EcsRamRoleTest. Specify the following request parameters for the operation:

    -   RoleName: the name of the RAM role. In this example, the RAM role is EcsRamRoleTest.
    -   AssumeRolePolicyDocument: Enter the following policy, which indicates that ECS instances can assume this RAM role:

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

2.  Grant the RAM role the permission to access KMS.

    Use OpenAPI Explorer to call the [AttachPolicyToRole](https://api.aliyun.com/#/?product=Ram&version=2015-05-01&api=AttachPolicyToRole) operation of RAM to attach the system policy AliyunKMSFullAccess to the RAM role EcsRamRoleTest. Specify the following request parameters for the operation:

    -   PolicyType: the type of the policy. Set this parameter to System, which indicates a system policy.
    -   PolicyName: the name of the KMS system policy. In this example, the system policy is AliyunKMSFullAccess.
    -   RoleName: the name of the RAM role. In this example, the RAM role is EcsRamRoleTest.

## Step 2: Assign the RAM role to an ECS instance

You can use one of the following methods to assign the RAM role to an ECS instance:

-   Assign the RAM role to an existing ECS instance.

    Use OpenAPI Explorer to call the [AttachInstanceRamRole](https://api.aliyun.com/#/?product=Ecs&version=2014-05-26&api=AttachInstanceRamRole) operation of ECS instances to assign the RAM role to an existing ECS instance in a Virtual Private Cloud \(VPC\). Specify the following request parameters for the operation:

    -   RegionId: the ID of the region where the ECS instance resides.
    -   RamRoleName: the name of the RAM role. In this example, the RAM role is EcsRamRoleTest.
    -   InstanceIds: the ID of the ECS instance in the VPC. Set this parameter to a value in the \["i-bXXXXXXXX"\] format.
-   Specify the RAM role when you create an ECS instance.
    1.  Create an instance.

        Use OpenAPI Explorer to call the [CreateInstance](https://api.aliyun.com/#/?product=Ecs&version=2014-05-26&api=CreateInstance) operation of ECS to create an ECS instance. Specify the following request parameters for the operation:

        -   RegionId: the ID of the region where the instance resides. In this example, the region ID is cn-hangzhou.
        -   ImageId: the ID of the image used by the instance. In this example, the image ID is centos\_7\_03\_64\_40G\_alibase\_20170503.vhd.
        -   InstanceType: the type of the instance. In this example, the type is ecs.g6.large.
        -   VSwitchId: the ID of the vSwitch in the VPC where the instance resides.

            **Note:** You can assign RAM roles only to ECS instances in VPCs. Therefore, this parameter is required.

        -   RamRoleName: the name of the RAM role. In this example, the RAM role is EcsRamRoleTest.
        You can also authorize a RAM user to use the RAM role. For more information, see [Use an instance RAM role by calling API operations](/intl.en-US/Security/Instance RAM roles/Use an instance RAM role by calling API operations.md).

    2.  Configure the password and start the instance.
    3.  Configure the instance to access the Internet in the ECS console or by calling an API operation.

## Step 3: \(Optional\) Obtain a temporary authorization token

You can obtain a temporary authorization token for the RAM role. You can use the permissions and resources granted to the RAM role by using this periodically updated token. To obtain a temporary authorization token, perform the following steps:

1.  Query the temporary authorization token of the RAM role EcsRamRoleTest.

    -   Linux instance: Run the `http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest` command.
    -   Windows instance: For more information, see [Overview](/intl.en-US/Instance/Manage instances/Metadata/Overview.md).
2.  Obtain the temporary authorization token.

    Sample success response:

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


## Step 4: Access KMS by using an SDK

You can use an SDK to access KMS in one of the following methods:



