# Enable deletion protection

If you enable deletion protection for a customer master key \(CMK\), the CMK cannot be deleted regardless of whether you use the Key Management Service \(KMS\) console or call API operations. This prevents CMKs from being deleted by mistake. This topic describes how to enable deletion protection.

A CMK is created. The CMK is not in the Pending Deletion state. For more information, see [Create a CMK](/intl.en-US/Quick Start/Manage and use keys/Create a CMK.md).

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the top navigation bar, select the region where your CMK resides.

3.  In the left-side navigation pane, click **Keys**.

4.  Find your CMK and click its name.

5.  In the **Key Details** section, click **Enable Deletion Protection**.

    **Note:** You can also click **Disable Deletion Protection** to disable deletion protection for your CMK.

6.  In the Enable message, click **OK**.

    After deletion protection is enabled, the status of Deletion Protection changes from **Disabled** to **Enabled**.


