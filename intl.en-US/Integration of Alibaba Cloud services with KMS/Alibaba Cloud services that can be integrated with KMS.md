# Alibaba Cloud services that can be integrated with KMS

This topic describes the Alibaba Cloud services that can be integrated with Key Management Service \(KMS\). These Alibaba Cloud services can use service keys or user-managed keys, including the keys imported by using the Bring Your Own Key \(BYOK\) feature, to encrypt data of different types in different scenarios.

## Workload data encryption

|Service|Description|Related topic|
|-------|-----------|-------------|
|Elastic Compute Service \(ECS\)|By default, the disk encryption feature of ECS uses a service key to encrypt your data. This feature can also use user-managed keys to encrypt your data. Each disk has its own customer master key \(CMK\) and data key \(DK\) and uses the envelope encryption mechanism to encrypt your data.

An ECS instance automatically encrypts the data transmitted to an encrypted disk and decrypts data read from the disk. Data is encrypted or decrypted on the host where the ECS instance resides. During encryption and decryption, the performance of the disk is almost not affected.

After an encrypted disk is created and attached to an ECS instance, the ECS instance encrypts the following data:

-   Static data stored on the disk.
-   Data transmitted between the disk and the ECS instance. Data in the operating system of the ECS instance is not encrypted.
-   All snapshots created from the encrypted disk. These snapshots are called encrypted snapshots.

|[Encryption overview](/intl.en-US/Block Storage/Encrypt a disk/Encryption overview.md)|
|Container Service for Kubernetes \(ACK\)|ACK supports server-side encryption \(SSE\) based on KMS for following types of workload data:

-   Kubernetes Secrets

In a Kubernetes cluster, [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/) are used to store and manage sensitive business data, such as application passwords, Transport Layer Security \(TLS\) certificates, and credentials to download Docker images. Kubernetes stores Secrets in etcd of the cluster.

-   Volumes

A volume can be a disk, OSS bucket, or Apsara File Storage NAS volume. You can use the specific SSE encryption method of KMS to encrypt each type of volumes. For example, you can create an encrypted disk and attach the disk to a Kubernetes cluster as a volume.


|[Use KMS to encrypt Kubernetes secrets at rest in the etcd](/intl.en-US/User Guide for Kubernetes Clusters/Introduction/Use KMS to encrypt Kubernetes secrets at rest in the etcd.md)|
|Web App Service|Web App Service is integrated with KMS to encrypt sensitive configuration data, such as access credentials of ApsaraDB RDS.

|[ApsaraDB for RDS instances](/intl.en-US/Managing Environments/Configure a deployment environment/ApsaraDB for RDS instances.md)|
|Application Configuration Management \(ACM\)|ACM is integrated with KMS to encrypt application configurations. This ensures the security of sensitive configurations, such as data sources, tokens, usernames, and passwords, and reduces the risk of configuration leak. ACM can use KMS in one of the following ways:

-   Encrypt data in KMS

ACM calls a data encryption API operation to transmit configurations to KMS. Then, KMS encrypts the configurations by using a specified CMK.

-   Use the envelope encryption mechanism to encrypt data in ACM

ACM uses a DK to encrypt configurations and calls a KMS API operation to encrypt the DK by using a specified CMK.


|[t15961.md\#](/intl.en-US/User Guide/Create and use encrypted configuration.md)|

## Persistent storage data encryption

|Service|Description|Related topic|
|-------|-----------|-------------|
|Object Storage Service \(OSS\)|OSS uses the SSE feature to encrypt uploaded data.

-   When you upload data to OSS, OSS encrypts the uploaded data and then stores the encrypted data in persistent storage.
-   When you download data from OSS, OSS automatically decrypts the encrypted data and returns the decrypted data to you. In addition, OSS declares that the data has been encrypted on the server in a header of the returned HTTP response.

OSS can use an encryption system dedicated to OSS to implement the SSE feature. In this case, this feature is called SSE-OSS. The keys used in this encryption system are not managed by OSS. Therefore, you cannot use ActionTrail to audit the use of these keys.

OSS can also use KMS to implement the SSE feature. In this case, this feature is called SSE-KMS. OSS uses the service key or user-managed keys to encrypt your data. OSS allows you to configure a default CMK for each bucket or specify the CMK to use when you upload an object.

|-   [Server-side encryption](/intl.en-US/Developer Guide/Data security/Data encryption/Server-side encryption.md)
-   [SDK reference](/intl.en-US/SDK Reference/Python/Data encryption/Server-side encryption.md) |
|Apsara File Storage NAS|By default, Apsara File Storage NAS uses the service key to encrypt your data. Each volume has its own CMK and DK and uses the envelope encryption mechanism to encrypt your data.

|[Encrypt data]()|
|Tablestore|By default, the encryption feature of Tablestore uses the service key to encrypt your data. This feature can also use user-managed keys to encrypt your data. Each table has its own CMK and DK and uses the envelope encryption mechanism to encrypt your data.

|N/A|
|Cloud Storage Gateway \(CSG\)|CSG supports the following encryption methods:

-   Gateway encryption: Files in the gateway cache are encrypted before they are uploaded to OSS.
-   OSS-based SSE

|-   [Enable gateway encryption](/intl.en-US/User Guide (Alibaba Cloud)/File Gateway/Enable gateway encryption.md)
-   [Manage shares](/intl.en-US/User Guide (Alibaba Cloud)/File Gateway/Manage shares.md) |

## Database encryption

|Service|Description|Related topic|
|-------|-----------|-------------|
|ApsaraDB RDS|ApsaraDB RDS supports the following encryption methods: -   Disk encryption

For disks used by ApsaraDB RDS instances, Alibaba Cloud provides the disk encryption feature for free. This feature encrypts disks based on block storage. The keys used for disk encryption are encrypted and stored in KMS. ApsaraDB RDS reads the keys only when you start or migrate instances.

-   Transparent data encryption \(TDE\)

ApsaraDB RDS for MySQL and ApsaraDB RDS for SQL Server support TDE. The keys used for TDE are encrypted and stored in KMS. ApsaraDB RDS reads the keys only when you start or migrate instances. After TDE is enabled for an ApsaraDB RDS instance, you can specify the database or table to be encrypted. The data of the specified database or table is first encrypted and then written to the destination device such as a disk, solid-state drive \(SSD\), or Peripheral Component Interconnect Express \(PCIe\) card, or to a service such as OSS. All data files and backups of the ApsaraDB RDS instance are stored in ciphertext.


|-   ApsaraDB RDS for MySQL: [Configure disk encryption for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure disk encryption for an ApsaraDB RDS for MySQL instance.md) and [Configure TDE for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure TDE for an ApsaraDB RDS for MySQL instance.md)
-   ApsaraDB RDS for SQL Server: [Configure disk encryption for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data security/Configure disk encryption for an ApsaraDB RDS for SQL Server instance.md) and [Configure TDE for an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Data security/Configure TDE for an ApsaraDB RDS for SQL Server instance.md)
-   ApsaraDB RDS for PostgreSQL: [Configure data encryption for an RDS PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Data security/Configure data encryption for an RDS PostgreSQL instance.md) |
|ApsaraDB for MongoDB|The encryption methods for ApsaraDB for MongoDB are similar to those for ApsaraDB RDS.

|[Configure TDE for an ApsaraDB for MongoDB instance](/intl.en-US/User Guide/Data security/Configure TDE for an ApsaraDB for MongoDB instance.md)|
|PolarDB|The encryption methods for PolarDB are similar to those for ApsaraDB RDS.|-   PolarDB for MySQL: [Configure TDE](/intl.en-US/User Guide/Data Security and Encryption/Configure TDE.md)
-   PolarDB-O: [Configure TDE for a PolarDB-O instance](https://www.alibabacloud.com/help/zh/doc-detail/164154.html)
-   PolarDB for PostgreSQL: [Set TDE]() |

## Log data encryption

|Service|Description|Related topic|
|-------|-----------|-------------|
|ActionTrail|When you create a single-account or multi-account trail, you can enable encryption for events in the ActionTrail console if the events are delivered to an OSS bucket.

|-   [Create a single-account trail](/intl.en-US/Single-account Trail Management/Create a single-account trail.md)
-   [Create a multi-account trail](/intl.en-US/Multi-account Trail Management/Create a multi-account trail.md) |
|Log Service|Log Service allows you to use KMS to encrypt data for secure storage.

|[Encrypt data](/intl.en-US/Developer Guide/API Reference/Common resources/Encrypt data.md)|

## Big data and AI

|Service|Description|Related topic|
|-------|-----------|-------------|
|MaxCompute|MaxCompute uses the service key or user-managed keys to encrypt your data.

|[Data encryption](/intl.en-US/Management/Data encryption.md)|
|Machine Learning Platform for AI \(PAI\)|You can configure SSE for the Alibaba Cloud services that are used in different data flow stages in the architecture of PAI, such as computing engines, ACK, and data storage services. This protects data security and privacy.|N/A|

## More scenarios

|Service|Description|Related topic|
|-------|-----------|-------------|
|Alibaba Cloud CDN|When an OSS Bucket is used as the origin, you can use OSS-based SSE to protect distributed content. For more information about how to allow CDN to access an encrypted bucket, see the CDN documentation.|[Configure private bucket back-to-origin authorization](/intl.en-US/Domain Management/Back-to-origin settings/Configure private bucket back-to-origin authorization.md)|
|ApsaraVideo for Media Processing|ApsaraVideo for Media Processing supports two encryption methods: Alibaba Cloud proprietary cryptography and HTTP Live Streaming \(HLS\) encryption. No matter which encryption method is used, ApsaraVideo for Media Processing can be integrated with KMS to protect video content.

|N/A |
|ApsaraVideo VOD|ApsaraVideo VOD supports two encryption methods: Alibaba Cloud proprietary cryptography and HLS encryption. No matter which encryption method is used, ApsaraVideo VOD can be integrated with KMS to protect video content.

|-   [Alibaba Cloud proprietary cryptography](https://www.alibabacloud.com/help/zh/doc-detail/68613.htm)
-   [HLS encryption](https://www.alibabacloud.com/help/zh/doc-detail/68612.htm) |

