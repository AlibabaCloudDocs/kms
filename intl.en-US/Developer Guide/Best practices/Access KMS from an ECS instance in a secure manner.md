# Access KMS from an ECS instance in a secure manner

You can create a Resource Access Management \(RAM\) role for an Elastic Compute Service \(ECS\) instance. Then, applications on the ECS instance can access Key Management Service \(KMS\) by using SDKs or a temporary access credential provided by Security Token Service \(STS\).

## Step 1: Create an instance RAM role and grant the required permissions to the role

1.  Create an instance RAM role.

    Call the [CreateRole](https://next.api.aliyun.com/api/Ram/2015-05-01/CreateRole) operation of RAM to create the EcsRamRoleTest RAM role by using OpenAPI Explorer. Specify the following request parameters for the operation:

    -   RoleName: the name of the instance RAM role. In this example, enter EcsRamRoleTest.
    -   AssumeRolePolicyDocument: the content of the policy that specifies an ECS instance to assume the RAM role. In this example, enter the following content:

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

2.  Grant the instance RAM role the permissions to access KMS.

    Call the [AttachPolicyToRole](https://next.api.aliyun.com/api/Ram/2015-05-01/AttachPolicyToRole) operation of RAM to attach the AliyunKMSFullAccess system policy to the EcsRamRoleTest RAM role by using OpenAPI Explorer. Specify the following request parameters for the operation:

    -   PolicyType: the type of the policy. Set this parameter to System, which indicates a system policy.
    -   PolicyName: the name of the system policy. In this example, enter AliyunKMSFullAccess, which indicates a system policy for KMS.
    -   RoleName: the name of the instance RAM role. In this example, enter EcsRamRoleTest.

## Step 2: Assign the instance RAM role to an ECS instance

You can use one of the following methods to assign the instance RAM role to an ECS instance:

-   Assign the instance RAM role to an existing ECS instance.

    Call the [AttachInstanceRamRole](https://next.api.aliyun.com/api/Ecs/2014-05-26/AttachInstanceRamRole) operation of ECS to assign the instance RAM role to an existing ECS instance in a virtual private cloud \(VPC\) by using OpenAPI Explorer. Specify the following request parameters for the operation:

    -   RegionId: the ID of the region where the ECS instance resides.
    -   RamRoleName: the name of the instance RAM role. In this example, enter EcsRamRoleTest.
    -   InstanceIds: the ID of the ECS instance in a VPC. Set this parameter to a value in the \["i-bXXXXXXXX"\] format.
-   Specify the instance RAM role when you create an ECS instance.
    1.  Create an ECS instance.

        Call the [CreateInstance](https://next.api.aliyun.com/api/Ecs/2014-05-26/CreateInstance) operation of ECS to create an ECS instance by using OpenAPI Explorer. Specify the following request parameters for the operation:

        -   RegionId: the ID of the region where you want to create the ECS instance. In this example, enter cn-hangzhou.
        -   ImageId: the ID of the image used to create the ECS instance. In this example, enter centos\_7\_03\_64\_40G\_alibase\_20170503.vhd.
        -   InstanceType: the type of the ECS instance. In this example, enter ecs.g6.large.
        -   VSwitchId: the ID of the vSwitch in the VPC where you want to create the ECS instance.

            **Note:** You can assign instance RAM roles to ECS instances only in VPCs. Therefore, this parameter is required.

        -   RamRoleName: the name of the instance RAM role. In this example, enter EcsRamRoleTest.
        You can also authorize a RAM user to assume the RAM role. For more information, see [Use an instance RAM role by calling API operations](/intl.en-US/Security/Instance RAM roles/Use an instance RAM role by calling API operations.md).

    2.  Set the password and start the ECS instance.
    3.  Allow the ECS instance to access the Internet in the ECS console or by calling an API operation.

## Step 3: \(Optional\) Obtain a temporary access credential

You can obtain a temporary access credential for the RAM role. The credential contains a token and is updated on a regular basis. The credential allows you to use the permissions and resources granted to the RAM role. To obtain a temporary access credential, perform the following steps:

1.  Query the temporary access credential of the EcsRamRoleTest RAM role.

    -   Linux ECS instance: Run the `http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest` command.
    -   Windows ECS instance: For more information, see [Overview of ECS instance metadata](/intl.en-US/Instance/Manage instances/Manage instance metadata/Overview of ECS instance metadata.md).
2.  Obtain the temporary access credential.

    Example of a temporary access credential:

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



