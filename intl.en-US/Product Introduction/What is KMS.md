# What is KMS {#concept_28935_zh .concept}

Key Management Service \(KMS\) supports secure key creation and key management. KMS provides security practices such as key rotation. Other cloud services can be integrated into KMS to encrypt the user data that KMS manages. With KMS, you can focus on developing services such as data encryption, data decryption, and digital signature verification. It helps you save costs in maintaining the security, integrity, and availability of your keys.

## Scenarios {#section_mwm_xmv_3x9 .section}

|User role|Scenario|KMS solution|
|:--------|:-------|:-----------|
|Application and website developers|Application and website developers need to use keys and certificates to encrypt data and sign signatures. They need a secure and independent key management service which can enable their applications to securely access keys at any place. They want to keep plaintext keys confidential.|KMS uses the envelope encryption mechanism. Customer master keys \(CMKs\) are stored in KMS. Only ciphertext data keys are installed on user servers. When a server wants to decrypt a data key, it only needs to call the KMS service.|
|Service providers|Service providers need to encrypt and protect user data used in their services. Service providers want to focus on developing business functions. They do not want to spend additional time and costs in developing key management and distribution functions. In addition, customers want the data encryption and protection functions provided by service providers to be manageable and reliable.| -   Administrators \(users\): use KMS to generate keys and manage the lifecycle of keys, and use Resource Access Management \(RAM\) to manage access permissions to keys.
-   Service providers: integrate the KMS API into their services and use user-specified keys to encrypt data.
-   Auditors \(users\): use ActionTrail to audit activities of accessing keys managed in KMS.

 |
|Chief security officers \(CSOs\)|CSOs want their key management services to comply with the security requirements and regulations of their enterprises. They want to implement key usage authorization. All key usage activities must be audited.| -   KMS provides managed Hardware Security Modules \(HSMs\). Managed HSMs are authority-certified third-party devices running in an approved security mode. You can use managed HSMs to generate keys, or import keys to managed HSMs to protect the keys.
-   KMS is integrated with Resource Access Management \(RAM\) to implement unified authentication and authorization.

 |

## Benefits {#section_3bo_sa5_ckh .section}

|Benefit|Traditional key management solution|KMS solution|
|:------|:----------------------------------|:-----------|
|Cost-effectiveness|The hardware and software costs for key management are high. For hardware, you have to purchase key management devices and build a physical environment. For software, you have to create and maintain key management regulations.|KMS is billed based on the actual usage with a customer favored price.|
|Easy to use| -   No standard connector is provided for calling the functions of key management devices.
-   It is complex to establish and maintain encrypted connections.

 | -   KMS provides a unified and easy-to-use API for you to call all the functions.
-   KMS uses the standard HTTPS protocol.

 |
|Reliability|Typically, data is backed up on local devices to guarantee high reliability.|KMS uses distributed systems and HSMs to guarantee high reliability.|

