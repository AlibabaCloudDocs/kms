# What is Key Management Service?

Key Management Service \(KMS\) is a one-stop service platform for key management and data encryption. KMS provides simple, reliable, secure, and standard-compliant capabilities to encrypt and protect data. KMS greatly reduces your costs of purchase, operations and maintenance \(O&M\), and research and development \(R&D\) on cryptographic infrastructure and data encryption services. This helps you focus on the business development.

## Architecture

KMS consists of the key service and Secrets Manager components.

|Component|Description|Related topic|
|---------|-----------|-------------|
|Key service|The key service provides fully managed keys and key protection features. The key service supports simple data encryption and digital signature management based on cloud-native API operations.|[CMK overview](/intl.en-US/Key Service/CMK overview.md)|
|Secrets Manager|Secrets Manager provides the secret encryption, hosting, regular rotation, secure distribution, and centralized management features. Secrets Manager reduces the security risks caused by static secrets that are configured in traditional IT facilities.|[Overview](/intl.en-US/Secrets Manager/Overview.md)|

## Benefits

KMS provides the benefits of data encryption and secret protection.

|Feature|Benefit|Description|Related topic|
|-------|-------|-----------|-------------|
|Data encryption|Leading security compliance capabilities|KMS supports industry-leading infrastructures of cryptographic security and meets the level and compliance requirements for cryptographic security both in and outside China.

|[Compliance](/intl.en-US/Key Service/Managed HSM/Overview.md)|
|Fully managed|Without the need to purchase cryptographic hardware and software, or invest in O&M and R&D of cryptographic facilities, you can directly use the data encryption feature and extend the feature.

|[Use Managed HSM](/intl.en-US/Key Service/Managed HSM/Use Managed HSM.md)|
|Cloud-native|Based on simple cloud-native API operations, KMS can be integrated with a variety of Alibaba Cloud services. KMS allows you to configure server-side encryption \(SSE\) with only a few clicks.

|[Alibaba Cloud services that can be integrated with KMS](/intl.en-US/Integration of Alibaba Cloud services with KMS/Alibaba Cloud services that can be integrated with KMS.md)|
|Simple application access|KMS provides multiple methods such as KMS SDK and Encryption SDK to help you use KMS API for encryption. This allows you to meet multiple requirements for data encryption and decryption, and digital signature generation and verification.

|-   [Code samples of SDK for Java](/intl.en-US/Developer Guide/KMS SDK/Code samples of SDK for Java.md)
-   [Quick start](/intl.en-US/Developer Guide/Encryption SDK/Quick start.md) |
|Centralized and large-scale management|KMS can be automatically activated and supports services such as Resource Orchestration Service \(ROS\) and Terraform to help you implement the default encryption policy on multi-account logon. KMS automatically enables SSE for services such as Elastic Compute Service \(ECS\) disks, Object Storage Service \(OSS\), ApsaraDB RDS, and MaxCompute.

|[Activate KMS by using the API](/intl.en-US/Quick Start/Activate KMS.md)|
|Secret protection|Cloud-native|KMS supports cloud-native dynamic ApsaraDB RDS secrets to help you handle the main security threats faced by databases.

|[t2005679.md\#]()|
|Simple application access|KMS provides multiple methods such as KMS SDK, Secrets Manager Client, and the Kubernetes plug-in to help you use dynamic secrets.

|[t2005667.md\#]()|
|Centralized and large-scale management|KMS can be automatically activated and supports services such as ROS and Terraform to help you implement automatic orchestration of Alibaba Cloud resources such as databases and OSS buckets, and automatic management of fully managed secrets. This way, centralized secret management is realized.

|[Activate KMS by using the API](/intl.en-US/Quick Start/Activate KMS.md)|

**Related topics**  


[Benefits](/intl.en-US/Product Introduction/Benefits.md)

[Scenarios](/intl.en-US/Product Introduction/Scenarios.md)

[Terms](/intl.en-US/Product Introduction/Terms.md)

[Limits](/intl.en-US/Product Introduction/Limits.md)

[Billing](/intl.en-US/Pricing/Billing.md)

[Overview](/intl.en-US/Quick Start/Overview.md)

