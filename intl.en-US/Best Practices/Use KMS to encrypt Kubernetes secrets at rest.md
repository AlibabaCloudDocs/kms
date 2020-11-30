# Use KMS to encrypt Kubernetes secrets at rest

Alibaba Cloud Container Service for Kubernetes \(ACK\) allows you to use a KMS customer master key \(CMK\) to encrypt the secrets of Kubernetes clusters at rest.

## Scenarios

ACK provides powerful capabilities in operation orchestration management. It obtains secrets such as passwords, certificates, credentials, and access keys across products, services, and modules. ACK uses secret modules to store and manage the sensitive information of Kubernetes clusters and that of business applications in the clusters. It also stores sensitive information in etcd. The replication feature of etcd supports distributed storage.

A Kubernetes cluster in the initialized state \(without any business load\) has about 50 secrets. The leak of any secret may cause immeasurable loss to the cluster, the business system, or even the entire enterprise. Therefore, you must protect the secrets hosted in Kubernetes clusters.

## Encryption mechanism

Professional managed Kubernetes clusters allow you to use a KMS CMK to encrypt secrets. The [KMS provider mechanism](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/) of Kubernetes is used during encryption. A KMS provider uses an envelope encryption scheme to encrypt or decrypt the keys of secrets that are stored in etcd. For more information about envelope encryption, see [What is envelope encryption?](/intl.en-US/FAQ/What is envelope encryption?.md). Key encryption and decryption procedures:

-   When you store a Kubernetes secret over the Kubernetes Secret API, the API server generates a random data key to encrypt your business key. Then, the system uses a KMS CMK to encrypt the data key and store the cyphertext of the data key in etcd.
-   When you decrypt the Kubernetes secret, the system calls the Decrypt API operation of KMS to decrypt the data key first. Then, the system uses the plaintext of the data key to decrypt the Kubernetes secret and returns the decrypted secret.

## Before you begin

-   Make sure that the ACK account is authorized to assume the AliyunCSManagedSecurityRole role. If you use an unauthorized account to enable secret encryption at rest for a new or existing professional managed Kubernetes cluster, you are prompted to authorize the account first.
-   If the current account is a RAM user, make sure that the RAM user has the AliyunKMSCryptoAdminAccess permission. For more information, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md).
-   Make sure that you have created a CMK in the KMS console. For more information, see [Create a CMK](/intl.en-US/Quick Start/Manage and use keys/Create a CMK.md).

    **Note:** Only CMKs of the Aliyun\_AES\_256 type are supported.


## Create a professional managed Kubernetes cluster and enable secret encryption at rest

1.  Log on to the [ACK console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**.

3.  In the upper-right corner of the Clusters page, click **Create Kubernetes Cluster**. In the Select Cluster Template panel, find the Professional Managed Cluster card and click **Create**.

4.  On the **ACK managed edition** tab, find **Secret Encryption**, select **Select Key**, and then select a CMK ID from the drop-down list.

    ![Encryption](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3559176061/p186311.png)

5.  Configure other parameters as prompted. For more information, see [Create an ACK Pro cluster](/intl.en-US/User Guide for Kubernetes Clusters/Introduction/Create an ACK Pro cluster.md).


## Enable secret encryption at rest for an existing professional managed Kubernetes cluster

1.  Log on to the [ACK console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**.

3.  On the Clusters page, click the name of the cluster for which you want to enable secret encryption at rest.

4.  Click the **Basic Information** tab. In the **Basic Information** section, turn on **Secret Encryption**.

    If the state of the cluster changes from **Updating** to **Running**, secret encryption at rest is enabled for the cluster.


## Results

If you can find encryption or decryption events performed by the AliyunCSManagedSecurityRole role on the **Query Event Details** page of the ActionTrail console, you have enabled secret encryption at rest for the cluster. You can view all the KMS CMK calling records in the ActionTrail console.

