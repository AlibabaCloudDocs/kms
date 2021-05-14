# Authorize Secrets Manager to manage AccessKey pairs of RAM users

To use Secrets Manager to manage Resource Access Management \(RAM\) secrets, you must authorize Secrets Manager to manage AccessKey pairs of RAM users. To do so, you can assign a RAM role with the specified permissions to Secrets Manager. This topic describes how to authorize Secrets Manager to manage AccessKey pairs of RAM users.

## Step 1: Create a custom policy

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using your Alibaba Cloud account.

2.  In the left-side navigation pane, choose **Permissions** \> **Policies**.

3.  On the Policies page, click **Create Policy**.

4.  Set the **Policy Name** parameter to **AliyunKMSManagedRAMCrendentialsRolePolicy**.

5.  Set the **Configuration Mode** parameter to **Script** and enter the following script in the **Policy Document** section:

    ```
    {
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "ram:ListAccessKeys",
                    "ram:CreateAccessKey",
                    "ram:DeleteAccessKey",
                    "ram:UpdateAccessKey"
                ],
                "Resource": "*"
            }
        ],
        "Version": "1"
    }
    ```

6.  Click **OK**.


## Step 2: Create a RAM role and attach the policy to it

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using your Alibaba Cloud account.

2.  In the left-side navigation pane, click **RAM Roles**.

3.  Create a RAM role.

    1.  On the RAM Roles page, click **Create RAM Role**.

    2.  In the Create RAM Role panel, select **Alibaba Cloud Service** for the Trusted entity type parameter and click **Next**.

    3.  Select **Normal Service Role** for the Role Type parameter.

    4.  Set the **RAM Role Name** parameter to **AliyunKMSManagedRAMCrendentialsRole**.

    5.  Select **Key Management Service** as the trusted service.

    6.  Click **OK**.

4.  Grant permissions to the RAM role.

    1.  In the Create RAM Role panel, click **Add Permissions to RAM Role** in the Finish step. The Add Permissions panel appears, in which the Principal parameter is automatically set.

    2.  In the **Select Policy** section, click **Custom Policy** and select the policy **AliyunKMSManagedRAMCrendentialsRolePolicy**.

    3.  Click **OK**.

    4.  Click **Complete**.


