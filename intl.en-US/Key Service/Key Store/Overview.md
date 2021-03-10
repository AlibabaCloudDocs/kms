# Overview

A key store is a security domain that is used to store keys in Key Management Service \(KMS\). Key stores contain created key metadata that is non-sensitive, and resources used for key storage and cryptographic operations. Key stores securely isolate keys and the resources that are used for key storage and cryptographic operations. This isolation meets the isolation standard of cryptography.

## Supported regions

Key stores are supported in the Singapore \(Singapore\) region.

## Benefits

KMS provides a default key store and allows you to create private key stores. Key stores allow you to manage and use keys in hardware security modules \(HSMs\) that belong to the same Alibaba Cloud account. Private key stores have the following benefits:

-   Compared with the default key store, private key stores use exclusive HSM resources to implement resource isolation and cryptographic isolation for higher security.
-   Private key stores reduce the complexity of using HSMs. Private key stores provide your HSMs with stable upper-layer key management and cryptographic operation services that are easy to use.
-   Private key stores allow you to integrate your HSMs with Alibaba Cloud services to provide higher security and controllability for encryption in Alibaba Cloud services. For more information, see [Alibaba Cloud services that can be integrated with KMS](/intl.en-US/Integration of Alibaba Cloud Services with KMS/Alibaba Cloud services that can be integrated with KMS.md).

## Architecture

Private key stores are associated with HSM clusters in Alibaba Cloud Data Encryption Service. The customer master keys \(CMKs\) in the private key stores are stored and used within HSM clusters. This provides higher security when you manage and use the keys.

![Architecture](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0582635161/p247594.png)

## Use a private key store

To use a private key store to manage your CMKs, perform the following steps:

1.  Log on to the [Data Encryption Service console](https://yundun.console.aliyun.com/?p=hsm) and perform the following steps:
    1.  Create an HSM cluster.
    2.  Add an HSM instance in the HSM cluster.
    3.  Initialize the HSM cluster. For more information, see [Initialize HSM](/intl.en-US/Quick Start/Step 6: Initialize HSM.md).
    4.  Create a crypto user named `kmsuser` and set a password for the `kmsuser` user. For more information, see [Create a crypto user](/intl.en-US/Quick Start/Step 8: Create a key.md).
2.  Log on to the [KMS console](https://kms.console.aliyun.com) and perform the following steps:
    1.  [Create a private key store](/intl.en-US/Key Service/Key Store/Create a private key store.md).
    2.  [Connect to a private key store](/intl.en-US/Key Service/Key Store/Connect to or disconnect from a private key store.md).
    3.  [Create a CMK](/intl.en-US/Quick Start/Manage and use keys/Create a CMK.md).

After the CMK is created, you can use the CMK in the HSM by using API operations, command-line interfaces \(CLIs\), or SDKs.

