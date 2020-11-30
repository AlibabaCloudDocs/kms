# Overview

Managed HSM is an important feature of Key Management Service \(KMS\) to enable easy access to certified hardware security modules \(HSMs\) provided by Alibaba Cloud.

An HSM is a highly secure hardware device that performs cryptographic operations and generates and stores keys. You can host the keys for your most sensitive Alibaba Cloud workloads and assets in HSMs that are managed on Alibaba Cloud \(referred to as managed HSMs\).

## Supported regions

You can use Managed HSM in the following regions. This feature is scheduled to be available in more regions in the future.

|Region|City|Certification type|Region ID|
|------|----|------------------|---------|
|China \(Beijing\)|Beijing|State Cryptography Administration \(SCA\) certification|cn-beijing|
|China \(Zhangjiakou\)|Zhangjiakou|SCA certification|cn-zhangjiakou|
|China \(Hangzhou\)|Hangzhou|SCA certification|cn-hangzhou|
|China \(Shanghai\)|Shanghai|SCA certification|cn-shanghai|
|China \(Shenzhen\)|Shenzhen|SCA certification|cn-shenzhen|
|China \(Hong Kong\)|Hong Kong|Federal Information Processing Standards \(FIPS\) 140-2 Level 3|cn-hongkong|
|Singapore \(Singapore\)|Singapore|FIPS 140-2 Level 3|ap-southeast-1|
|Australia \(Sydney\)|Sydney|FIPS 140-2 Level 3|ap-southeast-2|
|Malaysia \(Kuala Lumpur\)|Kuala Lumpur|FIPS 140-2 Level 3|ap-southeast-3|
|Indonesia \(Jakarta\)|Jakarta|FIPS 140-2 Level 3|ap-southeast-5|
|US \(Virginia\)|Virginia|FIPS 140-2 Level 3|us-east-1|

## Compliance

Managed HSM helps you meet regulatory requirements. Based on different regulatory requirements in each local market, Alibaba Cloud offers HSMs certified by different third-party organizations to meet both your localization and internationalization requirements.

For regions in mainland China:

-   SCA certification: Alibaba Cloud managed HSMs have passed the certification of the agencies designated by SCA.
-   SCA compliance: Alibaba Cloud managed HSMs comply with the relevant technical requirements and specifications of SCA and provide Alibaba Cloud users with commercial cryptographic algorithms that comply with both national and industrial standards.

For regions outside mainland China:

-   FIPS validation for hardware: Alibaba Cloud managed HSMs, including their hardware and firmware, have passed FIPS 140-2 Level 3 validation. For more information about the certificate issued by National Institute of Standards and Technology \(NIST\), visit [Certificate \#3254](https://csrc.nist.gov/Projects/Cryptographic-Module-Validation-Program/Certificate/3254).
-   FIPS 140-2 Level 3 compliance: Alibaba Cloud managed HSMs run in FIPS Approved Level 3 mode of operation.
-   PCI DSS: Alibaba Cloud managed HSMs comply with Payment Card Industry Data Security Standard \(PCI DSS\) requirements.

## High security assurance

-   Hardware protection

    Managed HSMs use secure hardware mechanisms to help you protect keys in KMS. The plaintext key material of CMKs is processed only inside HSMs for key operations. It is kept within the hardware security boundary of HSMs.

-   Secure key generation

    Randomness is crucial to the encryption strength of keys. Managed HSMs use a random number generation algorithm to generate key material. The algorithm is secure and licensed and has high system entropy seeds. This protects keys from being recovered or predicted by attackers.


## Ease of operation

HSM hardware is fully managed by Alibaba Cloud. This eliminates the costs otherwise incurred by the following hardware management operations:

-   Hardware lifecycle management
-   HSM cluster management
-   High availability and scalability management
-   System patching
-   Most disaster recovery operations

## Ease of integration

Native key management capabilities allow you to use the following features:

-   Key version management
-   Automatic key rotation
-   Resource tag management
-   Controlled authorization

These features enable rapid integration of your applications with HSMs, as well as the integration of ECS, ApsaraDB for RDS, and other cloud services with Managed HSM. You can implement cloud data encryption at rest without the need to pay any R&D costs.

## Key control

Managed HSM allows you to better control encryption keys on the cloud and move the most sensitive computing tasks and assets to the cloud.

If you use both Managed HSM and[BYOK \(Bring Your Own Key\)](https://www.alibabacloud.com/help/doc-detail/68523.htm), you can have full control over the following items:

-   Generation modes of key material.
-   Processing of key material: The key material that you import to a managed HSM can be destroyed but cannot be exported.
-   Lifecycle of keys.
-   Persistence of keys.

## Cost-effectiveness

You can benefit from the pay-as-you-go billing method of cloud computing. Compared with user-created key infrastructure by using your on-premises HSMs, Managed HSM eliminates hardware procurement costs, as well as subsequent R&D and O&M costs.

