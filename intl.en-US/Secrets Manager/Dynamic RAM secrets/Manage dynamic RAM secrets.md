# Manage dynamic RAM secrets

You can create a Resource Access Management \(RAM\) secret that is automatically rotated on a regular basis. This way, the risks of data leaks can be reduced. This topic describes how to create a dynamic RAM secret, delete a dynamic RAM secret, and restore a dynamic RAM secret that is scheduled for deletion in the Key Management Service \(KMS\) console.

-   The Alibaba Cloud account, RAM user, or RAM role for managing dynamic RAM secrets is obtained.

    If you use a RAM user or RAM role to manage dynamic RAM secrets, you must attach the system policies [AliyunKMSSecretAdminAccess](https://ram.console.aliyun.com/policies/AliyunKMSSecretAdminAccess/System/content) and [AliyunRAMFullAccess](https://ram.console.aliyun.com/policies/AliyunRAMFullAccess/System/content) to the RAM user or RAM role.

-   Secrets Manager is authorized to manage AccessKey pairs of RAM users. For more information, see [Authorize Secrets Manager to manage AccessKey pairs of RAM users](/intl.en-US/Secrets Manager/Dynamic RAM secrets/Authorize Secrets Manager to manage AccessKey pairs of RAM users.md).
-   An AccessKey pair is created for the RAM user for which you want to create a dynamic RAM secret. For more information, see [Create an AccessKey pair for a RAM user](/intl.en-US/Security Settings/AccessKey pairs/Create an AccessKey pair for a RAM user.md).

## Create a dynamic RAM secret

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region where you want to create a dynamic RAM secret.

3.  In the left-side navigation pane, click **Secrets**.

4.  Click **Create Secret**.

5.  In the Create Secret dialog box, configure the parameters and click **Next**.

    -   **Select Type**: Select **Managed RAM secret**.
    -   **Select RAM User**: Select the RAM user for which you want to create a dynamic RAM secret. The selected RAM user must have at least one AccessKey pair.
    -   **Set secret value**: Enter the AccessKey secret for the AccessKey ID that is displayed.

        **Note:** We recommend that you enter the correct AccessKey secret. If the AccessKey secret is invalid, you will obtain a new AccessKey ID and AccessKey secret after the dynamic RAM secret is rotated for the first time.

    -   **Secret Description**: Enter the description of the dynamic RAM secret.
6.  In the Configuration rotation step, select **Turn on automatic rotation**, set the **Rotation Period** parameter, and then click **Next**.

    **Note:** If you do not need to automatically rotate the dynamic RAM secret, select **Turn off automatic rotation**.

7.  In the Review and confirm step, check the configuration of the secret and click **OK**.

8.  In the Created successfully message, click **Close**.

    You can also click **View secret details** to view the secret information.


## Delete a dynamic RAM secret

Before you delete a dynamic RAM secret, make sure that the dynamic RAM secret is no longer used.

You can schedule the deletion of a dynamic RAM secret or immediately delete a dynamic RAM secret. When a dynamic RAM secret is deleted, the system does not delete the AccessKey pair of the RAM user that is associated with secret.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region where you want to delete a dynamic RAM secret.

3.  In the left-side navigation pane, click **Secrets**.

4.  Find the dynamic RAM secret that you want to delete and choose **More** \> **Plan Deletion Secret** in the **Actions** column.

5.  In the Delete Secret dialog box, select a method to delete the secret, and click **OK**.

    -   Select **Plan Deletion Secret** and set the **Delete In \(7 to 30 Days\)** parameter. The system deletes the secret after the specified number of days.

        Before the system deletes the secret, you can restore the secret to cancel deletion. For more information, see [Restore a dynamic RAM secret that is scheduled for deletion](#section_orf_p66_q3p).

    -   Select **Delete Secret Immediately**. The system immediately deletes the secret.

## Restore a dynamic RAM secret that is scheduled for deletion

After you schedule the deletion of a dynamic RAM secret and before the system deletes the secret, you can restore the secret to cancel deletion. After the dynamic RAM secret is restored, it can be used as normal.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region where you want to restore a dynamic RAM secret that is scheduled for deletion.

3.  In the left-side navigation pane, click **Secrets**.

4.  Find the dynamic RAM secret that you want to restore and choose **More** \> **Restore Secret** in the **Actions** column.

5.  In the Restore Secret message, click **OK**.


