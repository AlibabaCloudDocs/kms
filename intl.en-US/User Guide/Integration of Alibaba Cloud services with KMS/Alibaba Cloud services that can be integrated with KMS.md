# Alibaba Cloud services that can be integrated with KMS

This topic describes the Alibaba Cloud services that can be integrated with Key Management Service \(KMS\). These Alibaba Cloud services can use service keys or user-managed keys, including keys based on Bring Your Own Key \(BYOK\), to encrypt data.

Integration with KMS allows you to protect your data stored in Alibaba Cloud services at low costs, provides security boundaries for business data, and enhances the capabilities to protect business security in Alibaba Cloud. KMS can protect not only the business data that you can directly access, but also the business data that you can only indirectly access.

|Service|Description|Related topic|
|-------|-----------|-------------|
|Elastic Compute Service \(ECS\)|By default, the disk encryption feature of ECS uses a service key to encrypt your data. This feature also supports user-managed keys. Each disk has its own customer master key \(CMK\) and data key \(DK\) and uses the envelope encryption mechanism to encrypt your data.

An ECS instance automatically encrypts the data transmitted to an encrypted disk and decrypts data read from the disk. Data is encrypted or decrypted on the host where the ECS instance resides. During encryption and decryption, the performance of the disk is almost not affected.

After an encrypted disk is created and attached to an ECS instance, the ECS instance encrypts the following data:

-   Static data stored on the disk.
-   Data transmitted between the disk and the ECS instance. Data in the operating system of the ECS instance is not encrypted.
-   All snapshots created from the encrypted disk. These snapshots are called encrypted snapshots.

|[Encryption overview](/intl.en-US/Block Storage/Encrypt a disk/Encryption overview.md)|
|Object Storage Service \(OSS\)|OSS uses the server-side encryption \(SSE\) feature to encrypt uploaded data.

-   When you upload data to OSS, OSS encrypts the uploaded data and then stores the encrypted data in persistent storage.
-   When you download data from OSS, OSS automatically decrypts the encrypted data and returns the decrypted data to you. In addition, OSS declares that the data has been encrypted on the server in a header of the returned HTTP response.

OSS can use an encryption system dedicated to OSS to implement the SSE feature. In this case, this feature is called SSE-OSS. The keys used in this encryption system are managed by OSS. Therefore, you cannot use ActionTrail to audit the use of these keys.

OSS can also use KMS to implement the SSE feature. In this case, this feature is called SSE-KMS. OSS uses the service key or user-managed keys to encrypt your data. OSS allows you to configure a default CMK for each bucket or specify the CMK to use when you upload an object.

|-   [Server-side encryption](/intl.en-US/Developer Guide/Data security/Data encryption/Server-side encryption.md)
-   [SDK reference](/intl.en-US/SDK Reference/Python/Data encryption/Server-side encryption.md) |
|Container Service for Kubernetes \(ACK\)|In a Kubernetes cluster, [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/) are used to store and mange sensitive data, such as passwords to applications, Transport Layer Security \(TLS\) certificates, and credentials to download Docker images. Kubernetes stores Secrets in etcd of the cluster.

In clusters of ACK Pro, you can use a CMK that you created in KMS to encrypt Kubernetes Secrets.

|[Use KMS to encrypt Kubernetes Secrets](/intl.en-US/User Guide for Kubernetes Clusters/Security management/Use KMS to encrypt Kubernetes Secrets.md)|
|ApsaraDB for RDS|ApsaraDB for RDS supports the following methods to encrypt data: -   Disk encryption

For disks used by ApsaraDB for RDS instances, Alibaba Cloud provides the disk encryption feature for free. This feature encrypts disks based on block storage. The keys used for disk encryption are encrypted and stored in KMS. ApsaraDB for RDS reads the keys only when you start or migrate instances.

-   Transparent Data Encryption \(TDE\)

ApsaraDB RDS for MySQL and ApsaraDB RDS for SQL Server support TDE. The keys used for TDE are encrypted and stored in KMS. ApsaraDB for RDS reads the keys only when you start or migrate instances. After TDE is enabled for an ApsaraDB for RDS instance, you can specify the database or table to be encrypted. The data of the specified database or table is first encrypted and then written to the destination device such as a hard disk drive \(HDD\), solid-state drive \(SSD\), or Peripheral Component Interconnect Express \(PCIe\) card, or to a service such as OSS. All data files and backups of the ApsaraDB for RDS instance are stored in ciphertext.


|-   ApsaraDB RDS for MySQL: [Configure disk encryption for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure disk encryption for an ApsaraDB RDS for MySQL instance.md) and [Configure TDE for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)
-   ApsaraDB RDS for SQL Server: [Configure disk encryption for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data security/Configure disk encryption for an ApsaraDB RDS for SQL Server instance.md) and [Configure TDE for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data security/Configure TDE for an ApsaraDB RDS for SQL Server instance.md)
-   ApsaraDB RDS for PostgreSQL: [Configure data encryption for an RDS PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Data security/Configure data encryption for an RDS PostgreSQL instance.md) |
|ApsaraDB for MongoDB|The encryption method for ApsaraDB for MongoDB is similar to that for ApsaraDB for RDS.|[Configure TDE for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure TDE for an ApsaraDB for MongoDB instance.md)|
|PolarDB|The encryption method for PolarDB is similar to that for ApsaraDB for RDS.|[Configure TDE](/intl.en-US/User Guide/Data Security and Encryption/Configure TDE.md)|
|Apsara File Storage NAS|By default, Apsara File Storage NAS uses the service key to encrypt your data. Each volume has its own CMK and DK and uses the envelope encryption mechanism to encrypt your data.

|[Encrypt data]()|
|Tablestore|By default, the encryption feature of Tablestore uses the service key to encrypt your data. This feature also supports user-managed keys. Each table has its own CMK and DK and uses the envelope encryption mechanism to encrypt your data.

|None|
|MaxCompute|MaxCompute uses the service key as the CMK to encrypt your data.

|[Data encryption](/intl.en-US/Management/Data encryption.md)|
|Cloud Storage Gateway \(CSG\)|CSG supports two encryption methods:

-   Gateway encryption: Files in the gateway cache are encrypted before they are uploaded to OSS.
-   OSS server-side encryption.

|-   [Enable gateway encryption](/intl.en-US/User Guide (Alibaba Cloud)/File Gateway/Enable gateway encryption.md)
-   [Manage shares](/intl.en-US/User Guide (Alibaba Cloud)/File Gateway/Manage shares.md) |
|ApsaraVideo for Media Processing|ApsaraVideo for Media Processing supports two encryption methods: proprietary encryption and HLS standard encryption. No matter which encryption method is used, ApsaraVideo for Media Processing can be integrated with KMS to protect video content.

|None |
|ApsaraVideo for VOD|ApsaraVideo for VOD supports two encryption methods: Alibaba Cloud video encryption and HLS standard encryption. No matter which encryption method is used, ApsaraVideo for VOD can be integrated with KMS to protect video content.

|-   [Alibaba Cloud video encryption](https://www.alibabacloud.com/help/zh/doc-detail/68613.htm)
-   [HLS standard encryption](https://www.alibabacloud.com/help/zh/doc-detail/68612.htm) |
|Web App Service|Web App Service is integrated with KMS to encrypt sensitive configuration data, such as access credentials of ApsaraDB for RDS.

|[ApsaraDB for RDS instances](/intl.en-US/Managing Environments/Configure a deployment environment/ApsaraDB for RDS instances.md)|
|Application Configuration Management \(ACM\)|ACM is integrated with KMS to encrypt application configurations. This ensures the security of sensitive configurations, such as data sources, tokens, usernames, and passwords, and reduces the risk of configuration leakage. ACM can use KMS in one of the following ways:

-   Encrypt data in KMS

ACM calls a data encryption API operation to transmit configurations to KMS. Then, KMS encrypts the configurations with a specified CMK.

-   Use the envelope encryption mechanism to encrypt data in ACM

ACM uses a DK to encrypt configurations in ACM and calls a KMS API operation to encrypt the DK with a specified CMK.


|[Create and use encrypted configuration](/intl.en-US/User Guide/Create and use encrypted configuration.md)|

