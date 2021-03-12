# Create a private key store

Private key stores help you manage and use keys in hardware security modules \(HSMs\). This topic describes how to create a private key store.

Private key stores must be associated with HSM clusters in Alibaba Cloud Data Encryption Service within the same Alibaba Cloud account. Make sure that the following configurations are complete in Data Encryption Service:

1.  An HSM cluster is created.
2.  An HSM instance is added to the HSM cluster. We recommend that you add two or more HSM instances to ensure the high availability of the HSM cluster.
3.  The HSM cluster is initialized. After you initialize the HSM cluster, it enters the initialized state. The **ClusterOwnerCertificate** that you configure when you initialize the cluster is used as the security domain certificate for Key Management Service \(KMS\) to access the HSM cluster. For more information, see [Initialize the cluster](/intl.en-US/Quick Start/Step 7: Initialize the cluster.md).
4.  A crypto user named `kmsuser` is created and a password is set for the `kmsuser` user. KMS uses this user to access your HSM cluster, create keys, and perform cryptographic operations. For more information, see [Create a crypto user](/intl.en-US/Quick Start/Step 9: Create a key.md).

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region in which you want to create a private key store.

    For more information about the regions that support private key stores, see [Supported regions](/intl.en-US/Key Service/Key Store/Overview.md).

3.  In the left-side navigation pane, click **KeyStores**.

4.  Click **Create KeyStore**.

5.  In the Create KeyStore dialog box, set the following parameters:

    -   **Name**: Enter the name of the private key store.
    -   **HSM cluster**: Select the HSM cluster in Alibaba Cloud Data Encryption Service.
    -   **Description**: Enter the description of the private key store.
    -   **Password**: Enter the password that is set for the `kmsuser` user in Alibaba Cloud Data Encryption Service.
    -   **Security domain certificate**: Enter security information or upload the security domain certificate for the HSM cluster in Alibaba Cloud Data Encryption Service.
6.  Click **OK**.


By default, the private key store enters the disconnected state after it is created. To create a customer master key \(CMK\) in the private key store, you must connect to the private key store first. For more information, see the following topics:

1.  [Connect to a private key store](/intl.en-US/Key Service/Key Store/Connect to or disconnect from a private key store.md)
2.  [Create a CMK](/intl.en-US/Quick Start/Manage and use keys/Create a CMK.md)

