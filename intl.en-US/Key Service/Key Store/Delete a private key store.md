# Delete a private key store

This topic describes how to delete a private key store. After a private key store is deleted, you cannot manage and use the keys in the private key store by using Key Management Service \(KMS\). If your keys are used by online applications, this operation may affect online business. Proceed with caution.

Before you delete a private key store, make sure that the following requirements are met:

1.  The deletion is scheduled for all customer master keys \(CMKs\) in the private key store. For more information, see [Schedule the deletion of a CMK](/intl.en-US/Key Service/Manage CMKs/Schedule the deletion of a CMK.md).
2.  The private key store is disconnected after the CMKs are deleted. For more information, see [Disconnect from a private key store](/intl.en-US/Key Service/Key Store/Connect to or disconnect from a private key store.md).

**Note:** If you disconnect from the private key store before you schedule the deletion of the CMKs, KMS deletes key metadata that is non-sensitive from the private key store. However, the keys in hardware security modules \(HSMs\) cannot be deleted.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region where the private key store resides.

    For more information about the regions that support private key stores, see [t2045267.md\#section\_7lv\_d2x\_n03]().

3.  In the left-side navigation pane, click **KeyStores**.

4.  On the KeyStores page, find the private key store that you want to delete and click **Delete** in the **Actions** column.

5.  In the Delete KeyStore message, click **OK**.


