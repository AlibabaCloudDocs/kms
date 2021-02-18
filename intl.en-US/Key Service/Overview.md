# Overview

The key service is a core component of Key Management Service \(KMS\). The key service provides fully managed keys and key protection features. The key service supports simple data encryption and digital signature management based on cloud-native API operations.

## Key hosting and protection

|Feature|Description|Related topic|
|-------|-----------|-------------|
|Host and manage keys|An encryption key managed by KMS is called a customer master key \(CMK\). You can manage the lifecycle of a CMK.|-   [Create a CMK](/intl.en-US/Quick Start/Manage and use keys/Create a CMK.md)
-   [Disable a CMK](/intl.en-US/Key Service/Manage CMKs/Disable a CMK.md)
-   [Schedule the deletion of a CMK](/intl.en-US/Key Service/Manage CMKs/Schedule the deletion of a CMK.md) |
|You can rotate keys.|-   [Overview](/intl.en-US/Key Service/Rotate CMKs/Overview.md)
-   [Automatic key rotation](/intl.en-US/Key Service/Rotate CMKs/Automatic key rotation.md) |
|You can set an alias for a key to easily use the key. You can also manage keys by calling API operations.|-   [Overview](/intl.en-US/Key Service/Manage aliases/Overview.md)
-   [Key service operations](/intl.en-US/API Reference/List of operations by function.md) |
|Protect keys and meet compliance requirements|When you use keys, you must meet security and compliance requirements. We recommend that you set the protection level of your CMK to hardware security module \(HSM\) to protect the CMK by using dedicated hardware. This also allows keys to meet GM/T or FIPS 140-2 Level 3 compliance requirements. After the protection level of the CMK is set to HSM, the plaintext of the key material is stored only inside an HSM. No one can access the plaintext of the key material. The plaintext of the key material cannot be exported from the HSM.|-   [Overview](/intl.en-US/Key Service/Managed HSM/Overview.md)
-   [Use Managed HSM](/intl.en-US/Key Service/Managed HSM/Use Managed HSM.md) |
|Use Bring Your Own Key \(BYOK\)|You can import your own keys to KMS by using the BYOK feature to meet specific security requirements. Your own keys include keys managed offline, keys hosted in other clouds, keys used in Alibaba Cloud Data Encryption Service.|-   [Import key material](/intl.en-US/Key Service/Key type/Use symmetric keys/Import key material.md)
-   [Key control](/intl.en-US/Key Service/Managed HSM/Overview.md) |

## Data encryption

KMS provides cloud-native cryptographic API operations that are simpler than those for traditional cryptographic modules or cryptographic software libraries. In addition, KMS provides multiple SDKs to accelerate the development. For more information about how to use SDKs to develop code, see [Overview](/intl.en-US/Developer Guide/Overview.md).

|Feature|Description|Related topic|
|-------|-----------|-------------|
|Encrypt data for Alibaba Cloud services with a few clicks|KMS is integrated with a variety of Alibaba Cloud services and provides cloud-native encryption features. You only need to perform simple configurations to allow KMS to automatically encrypt your data in other Alibaba Cloud services.|-   [Integration with KMS](/intl.en-US/Integration of Alibaba Cloud Services with KMS/Integration with KMS.md)
-   [Alibaba Cloud services that can be integrated with KMS](/intl.en-US/Integration of Alibaba Cloud Services with KMS/Alibaba Cloud services that can be integrated with KMS.md) |
|Encrypt data for Alibaba Cloud services by using code|KMS SDKKMS SDK encapsulates KMS API operations. You can view the sample code to learn how to call the [Encrypt](/intl.en-US/API Reference/Key/Encrypt.md) operation of KMS in your code to encrypt data.

|[Sample code for data encryption](/intl.en-US/Quick Start/Manage and use keys/Sample code for data encryption.md)|
|Encryption SDKEncryption SDK is a client-side encryption library based on KMS API operations. You can view the quick start of Encryption SDK to learn how to call Encryption SDK in your code to use the envelope encryption feature.

|-   [Quick start of Encryption SDK for Java](/intl.en-US/Developer Guide/Encryption SDK/Quick Start/Quick start of Encryption SDK for Java.md)
-   [What is envelope encryption?](/intl.en-US/FAQ/What is envelope encryption?.md) |

## Description of encryption algorithms supported by KMS

The following table describes the encryption algorithms supported by KMS.

|Algorithm class|Algorithm subclass|Encryption and decryption|Signature generation and verification|
|---------------|------------------|-------------------------|-------------------------------------|
|Symmetric key algorithm|AES|Supported|Not supported|
|Symmetric key algorithm|SM4 Note|Supported|Not supported|
|Asymmetric key algorithm|RSA|Supported|Supported|
|Asymmetric key algorithm|ECC|Not supported|Supported|
|Asymmetric key algorithm|SM2 Note|Supported|Supported|

**Note:** Only managed HSMs in mainland China support the SM4 and SM2 algorithms. For more information, see [Supported regions](/intl.en-US/Key Service/Managed HSM/Overview.mdsection_9br_g7q_yb4).

Symmetric keys are used to encrypt or decrypt data. If you do not specify the KeySpec parameter during key creation, KMS creates a symmetric key. For more information, see [Overview](/intl.en-US/Key Service/Key type/Use symmetric keys/Overview.md).

Asymmetric keys can be used to encrypt data, decrypt data, generate a signature, or verify a signature. An asymmetric CMK in KMS consists of a public key and a private key, which are cryptographically related to each other. The public key can be sent to anyone, but the private key must be kept secure. KMS does not provide an API operation for you to export the private key of an asymmetric key pair. You can only call API operations to use the private key to generate signatures or decrypt data. For more information, see [Overview](/intl.en-US/Key Service/Key type/Use asymmetric keys/Overview.md).

