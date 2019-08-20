# Overview {#concept_1215941 .concept}

Managed HSM is an important feature of Key Management Service \(KMS\) to enable easy access to certified Hardware Security Modules \(HSMs\) provided by Alibaba Cloud.

An HSM is a hardware device that performs cryptographic operations, and generates and stores keys. You can protect your most sensitive workloads and assets provided by Alibaba Cloud, by hosting keys in these highly secure hardware devices.

## Supported regions {#section_9br_g7q_yb4 .section}

You can use Managed HSM in the following regions. This feature will be provided in more regions later.

|Region|City|Region ID|
|------|----|---------|
|China（Hong Kong）|Hong Kong|cn-hongkong|
|Singapore|Singapore|ap-southeast-1|

## Regulatory compliance {#section_vyz_io3_a0v .section}

Managed HSM can help you meet stringent regulatory requirements. Based on different regulatory requirements in each local market, Alibaba Cloud offers HSMs certified by different third-party organizations to meet your localization and internationalization requirements.

For regions outside mainland China,

-   FIPS validation for hardware: Alibaba Cloud HSMs, including their hardware and firmware, have passed FIPS 140-2 Level 3 validation. For more information, see [Certificate \#3254](https://csrc.nist.gov/Projects/Cryptographic-Module-Validation-Program/Certificate/3254).
-   FIPS 140-2 Level 3 Compliance: Alibaba Cloud Managed HSM runs under FIPS Approved Level 3 mode of operation.
-   PCI DSS: Alibaba Cloud Managed HSM complies with PCI SS requirements.

## High security assurance {#section_tci_i9g_7i7 .section}

-   Hardware protection

    Managed HSM helps you protect keys in KMS through hardware mechanisms. The plaintext key material of CMKs is only processed inside HSMs for key operations. It is kept within the hardware security boundary of HSMs.

-   Secure key generation

    Randomness is crucial to the encryption strength of keys. Managed HSM uses a random number generation algorithm that is secure and licensed and has high system entropy seeds to generate key material. This protects keys from being recovered or predicted by attackers.


## Ease of operation {#section_bu2_gho_3er .section}

Alibaba Cloud fully manages HSM hardware. This eliminates the costs otherwise incurred by the following hardware management operations:

-   Hardware lifecycle management
-   HSM cluster management
-   High availability and scalability management
-   System patching
-   Most disaster recovery operations

## Ease of integration {#section_kd9_j50_2nx .section}

Native key management capabilities allow you to use the following features:

-   Key version management
-   Automatic key rotation
-   Resource tag management
-   Controlled authorization

These features enable rapid integration of your applications with HSMs, as well as integration of ECS, RDS, and other cloud services with Managed HSM. You can implement static encryption of cloud data without paying any R&D costs.

## Key control {#section_x1y_emf_972 .section}

Managed HSM allows you to better control encryption keys on the cloud and move the most sensitive computing tasks and assets to the cloud.

When using both Managed HSM and [Bring Your Own Key \(BYOK\)](https://partners-intl.aliyun.com/help/doc-detail/68523.htm), you can have full control over the following items:

-   How key material is generated
-   The key material that you import to the managed HSM cannot be exported, but can be destroyed.
-   Key lifecycle
-   Key persistence

## Low cost {#section_9ya_jyy_hcx .section}

You can benefit from the pay-as-you-go billing method of cloud computing. Compared with user-created key infrastructure by using local HSMs, Managed HSM eliminates hardware procurement costs, as well as subsequent R&D and O&M costs.

