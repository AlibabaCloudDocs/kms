# Schedule the deletion of a CMK

After a CMK is deleted, it cannot be recovered, and the data and ciphertext data keys encrypted by using this CMK cannot be decrypted. Therefore, to prevent you from deleting CMKs by mistake, KMS only allows you to schedule key deletion tasks. You cannot immediately delete CMKs. Rather than deleting a CMK, we recommend that you disable the CMK.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the top navigation bar, select the region where your CMK resides.

3.  In the left-side navigation pane, click **Keys**.

4.  Find the CMK for which you want to schedule deletion, and choose **More** \> **Schedule Key Deletion** in the **Actions** column.

5.  In the Schedule Key Deletion dialog box, specify **Delete In \(7-30 days\)**.

    The value ranges from 7 to 30. Unit: days. Default value: 30.

6.  Click **OK**.

    **Note:**

    -   The CMK state changes from **Enabled** to **Pending Deletion**. A CMK in the **Pending Deletion** state cannot be used to encrypt data, decrypt data, or generate data keys.
    -   You can choose **More** \> **Cancel Key Deletion** in the Actions column to cancel the scheduled key deletion task.

