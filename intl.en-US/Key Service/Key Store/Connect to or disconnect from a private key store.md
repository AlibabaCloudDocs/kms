# Connect to or disconnect from a private key store

This topic shows you how to connect to or disconnect from a private key store.

## Connect to a private key store

If you need to create a customer master key \(CMK\) in a private key store after the private key store is created, you must connect to the private key store first.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region where the private key store resides.

    For more information about the regions that support private key stores, see [t2045267.md\#section\_7lv\_d2x\_n03]().

3.  In the left-side navigation pane, click **KeyStores**.

4.  On the KeyStores page, find the private key store to which you want to connect and click **Connect** in the **Actions** column.

    After you connect to the private key store, the private key store enters the connected state. Then, you can create a CMK in the private key store. For more information, see [Create a CMK](/intl.en-US/Quick Start/Manage and use keys/Create a CMK.md).


## Disconnect from a private key store

To delete a private key store, you must disconnect from the private key store first.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region where the private key store resides.

    For more information about the regions that support private key stores, see [t2045267.md\#section\_7lv\_d2x\_n03]().

3.  In the left-side navigation pane, click **KeyStores**.

4.  On the KeyStores page, find the private key store from which you want to disconnect and click **Disconnect** in the **Actions** column.

5.  In the Disconnect KeyStore message, click **OK**.

    After you disconnect from the private key store, the private key store enters the disconnected state. Then, you cannot create or use a CMK in the private key store, but you can delete existing CMKs from the private key store.


