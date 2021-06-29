# Manage dynamic ECS secrets

You can create dynamic Elastic Compute Service \(ECS\) secrets and manually rotate the ECS secrets to reduce the risk of ECS secret leaks. Secrets Manager can also automatically rotate ECS secrets on a regular basis. This topic describes how to create, rotate, and delete a dynamic ECS secret, and restore a dynamic ECS secret that is scheduled for deletion in the Key Management Service \(KMS\) console.

-   ECS instances are created. For more information, see [Create an ECS instance](/intl.en-US/Instance/Create an instance/Creation method overview.md).
-   The Alibaba Cloud account, RAM user, or RAM role for managing dynamic ECS secrets is obtained.

    If a RAM user or RAM role is used to manage secrets, the system policy [AliyunKMSSecretAdminAccess](https://ram.console.aliyun.com/policies/AliyunKMSSecretAdminAccess/System/content) is attached to the RAM user or RAM role. This policy grants the following permissions:

    -   The permission to use the features of Secrets Manager.
    -   The permission to query ECS instances.
    -   The permission to create the service-linked role used by dynamic ECS secrets.
    For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Authorization management/Grant permissions to a RAM user.md) and [Grant permissions to a RAM role](/intl.en-US/RAM Role Management/Grant permissions to a RAM role.md).


## Create a dynamic ECS Secret

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the top navigation bar, select the region where you want to create a secret.

    **Note:** The region of the secret must be the same as that of the ECS instance for which you want to create the secret.

3.  In the left-side navigation pane, click **Secrets**.

4.  Click **Create Secret**.

5.  In the Create Secret dialog box, configure the parameters and click **Next**.

    -   **Select Type**: Select **Managed ECS secret**.
    -   **Secret name**: Enter the name of the secret.
    -   **Managed instance**: Select an existing ECS instance within your Alibaba Cloud account.
    -   **Managed User**: Enter the name of an existing user on the ECS instance, such as root for the Linux operating system or Administrator for the Windows operating system.
    -   **Initial secret value**: Select **Password** or **Key Pair** and enter the initial value.

        **Note:** If the initial value is invalid, you can obtain the valid password or key pair after the ECS secret is rotated for the first time.

    -   **Secret Description**: Enter the description of the ECS secret.
6.  In the Configuration rotation step, select **Turn on automatic rotation**, set the **Rotation Period** parameter, and then click **Next**.

    **Note:** If you do not need to automatically rotate the ECS secret, select **Turn off automatic rotation**.

7.  In the Review and confirm step, check the configuration of the secret and click **OK**.

    After the secret is created, it appears in the secret list and its **Secret Type** is **Managed ECS secret**.


## Rotate a dynamic ECS secret

If a dynamic ECS secret is leaked, you can immediately rotate the ECS secret in the KMS console to block intrusions.

1.  Click the name of the ECS secret that you want to rotate. On the secret details page, click **Rotate Immediately** in the upper-right corner.

2.  In the Prompt dialog box, turn on or off **Use Custom Secret**.

    -   If you turn on the switch, you need to specify a secret value.
    -   If you turn off the switch, KMS automatically creates a 32-character random password or RSA-2048 public-private key pair.
3.  Click **Confirm rotation**.

4.  In the Rotation triggered message, click **Close**.


## Delete a dynamic ECS secret

Before you delete a dynamic ECS secret, make sure that the ECS secret is no longer used.

You can schedule the deletion of a dynamic ECS secret or immediately delete a dynamic ECS secret. Deleting a dynamic ECS secret does not affect the passwords or SSH keys that have been configured on the ECS instance.

1.  Find the dynamic ECS secret that you want to delete and choose **More** \> **Plan Deletion Secret** in the **Actions** column.

2.  In the Delete Secret dialog box, select a method to delete the secret, and click **OK**.

    -   Select **Plan Deletion Secret** and set the **Delete In \(7 to 30 Days\)** parameter. The system deletes the secret after the specified number of days.

        Before the system deletes the secret, you can restore the secret to cancel deletion. For more information, see [Restore a dynamic ECS secret that is scheduled for deletion](#section_orf_p66_q3p).

    -   Select **Delete Secret Immediately**. The system immediately deletes the secret.

## Restore a dynamic ECS secret that is scheduled for deletion

After you schedule the deletion of a dynamic ECS secret and before the system deletes the secret, you can restore the secret to cancel deletion. After the dynamic ECS secret is restored, it can be used as normal.

1.  Find the dynamic ECS secret that you want to restore and choose **More** \> **Restore Secret** in the **Actions** column.

2.  In the Restore Secret message, click **OK**.


