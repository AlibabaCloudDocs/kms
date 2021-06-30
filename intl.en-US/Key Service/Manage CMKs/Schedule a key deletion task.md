# Schedule a key deletion task

After a customer master key \(CMK\) is deleted, it cannot be recovered, and the data and ciphertext data keys encrypted by using this CMK cannot be decrypted. Therefore, to prevent you from deleting CMKs by mistake, KMS allows you only to schedule key deletion tasks. You cannot immediately delete CMKs. We recommend that you disable a CMK instead of deleting it.

A CMK is available. Deletion protection is disabled for the CMK. To disable deletion protection for a CMK, you can click **Disable Deletion Protection** in the Key Details section of the CMK. In the message that appears, click **OK**.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the top navigation bar, select the region where your CMK resides.

3.  In the left-side navigation pane, click **Keys**.

4.  Find the CMK for which you want to schedule a deletion task, and choose **More** \> **Schedule Key Deletion** in the **Actions** column.

5.  In the Schedule Key Deletion dialog box, specify **Delete In \(7-30 days\)**.

    Valid values of **Delete In \(7-30 days\)**: 7 to 30. Unit: days. Default value: 30.

6.  Click **OK**.

    **Note:**

    -   The CMK state changes from **Enabled** to **Pending Deletion**. A CMK in the **Pending Deletion** state cannot be used to encrypt data, decrypt data, or generate data keys.
    -   You can choose **More** \> **Cancel Key Deletion** in the Actions column to cancel the scheduled key deletion task.

