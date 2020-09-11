# Manage CMKs

This topic describes how to use Key Management Service \(KMS\) to create and manage customer master keys \(CMKs\). CMKs are used to encrypt data.

## Create a CMK

1.  Log on to the [KMS console](https://kms.console.aliyun.com)[KMS console](https://partners-intl.console.aliyun.com/#/kms).

2.  In the upper-left corner of the Keys page, click **Create Key**.

3.  In the Create Key dialog box, set **Alias Name** and **Description**.

4.  Click **Advanced** and specify **Key Material Source**.

    -   **Alibaba Cloud KMS**: Use KMS to generate key material.
    -   **External**: Import key material from an external source. For more information about how to import key material, see [Import and delete key material](/intl.en-US/User Guide/Use symmetric keys/Import and delete key material.md).

        **Note:** If you select External, you must also select **I understand the implications of using the external key materials key**.

5.  Click **OK**.


**Note:** After the CMK is created, you can view the detailed information, such as the CMK ID, status, and protection level on the Keys page.

## Disable a CMK

After you create a CMK, it is in the Enabled state by default. You cannot use a disabled CMK to encrypt or decrypt data. Follow these steps to disable a CMK:

1.  On the Keys page, find the CMK that you want to disable.

2.  In the **Actions** column, click **Disable**.

3.  In the Disable Key message, click **OK**.


## Schedule a key deletion task

After a CMK is deleted, it cannot be recovered, and the data and ciphertext data keys encrypted by using this CMK cannot be decrypted. Therefore, to prevent you from deleting CMKs by mistake, KMS only allows you to schedule key deletion tasks. You cannot immediately delete CMKs. Rather than deleting a CMK, we recommend that you disable the CMK.

1.  On the Keys page, find the CMK that you want to delete.

2.  In the **Actions** column, choose **More** \> **Schedule Key Deletion**.

3.  In the Schedule Key Deletion dialog box, specify **Delete In \(7-30 days\)**.

    The value ranges from 7 to 30. Unit: days. Default value: 30.****

4.  Click **OK**.


**Note:**

-   A CMK in the Pending Deletion state cannot be used to encrypt data, decrypt data, or generate data keys.
-   You can choose **More** \> **Cancel Key Deletion** to cancel a scheduled key deletion task.

