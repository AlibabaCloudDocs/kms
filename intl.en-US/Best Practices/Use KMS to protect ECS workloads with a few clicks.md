# Use KMS to protect ECS workloads with a few clicks

In most scenarios, the production data that you use Elastic Compute Service \(ECS\) workloads to process contains your business secrets, privacy information, or important credentials. Therefore, you must protect these workloads against information leaks. Key Management Service \(KMS\) supports quick encryption for ECS workloads to protect transient and persistent data generated in computing environments. This ensures data confidentiality and privacy and meets your requirements for compliance. KMS helps build a secure cloud computing environment at low costs.

## Background information

Customers have data security requirements on business secrets and personal privacy. These types of data are essential to enterprises and are subject to regulatory compliance. For example, General Data Protection Regulation \(GDPR\) requires enterprises to protect personal privacy data. The data is stored in databases. Before you store the data of an application system in databases, you must encrypt the data to reduce the risk of data leaks caused by attacks such as dictionary attacks.

To ensure the security and compliance of encryption, you can use KMS or Data Encryption Service to encrypt business data of an application system. For more information about how to encrypt your business data at the application layer, see [Use envelope encryption to encrypt and decrypt on-premises data](/intl.en-US/Best Practices/Use envelope encryption to encrypt and decrypt on-premises data.md).

If you have encrypted your business data, the workloads that are used to encrypt and decrypt data become a weak link in your system. Take note of the following points, which may cause security risks:

-   Your applications deployed on an ECS instance contain the important credentials that are used to access KMS, hardware security modules \(HSMs\), microservices, or subsystems.
-   The system disks of your ECS instances may generate some temporary files, including sensitive data files involved in network transmission and local data processing.
-   Disk backup based on automatic snapshot is enabled for your ECS instances to store multiple copies of sensitive data. This helps achieve data redundancy.

**Note:** The preceding risks are some examples. When you deploy business systems, other issues may occur. For example, if the application deployment and lifecycle change mechanisms are used in DevOps mode, O&M and security engineers are unaware of whether new types of sensitive data are generated for workloads. They cannot determine whether to introduce business logic to process the new sensitive data.

## Benefits

Alibaba Cloud ECS instances use KMS to protect the resources that ECS workloads require. The resources include system disks and data disks of ECS instances and relevant images and snapshots.

You can authorize ECS instances to use customer master keys \(CMKs\) in KMS and encrypt the resources with a few clicks. This protects known, potential, transient, and persistent sensitive data against unauthorized access. In emergencies, you can disable KMS-based decryption on an ECS instance by revoking permissions or disabling CMKs.

**Note:** O&M and security engineers can encrypt resources that ECS workloads require in DevOps mode. This is simple and efficient.

## Encrypt a system disk

A system disk contains the operating system and application software required for business operations. It is always packaged as an image.

After you create a custom image that can run in a production environment and use the custom image as a baseline, you can copy and encrypt the image. This way, an encrypted system disk is created.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.

3.  In the top navigation bar, select a region.

4.  On the **Images** page, click the **Custom Image** tab.

5.  Find your image and click **Copy Image** in the **Actions** column.

    **Note:** If the size of your image is greater than 500 GiB, you are prompted to submit a ticket to complete the operation when you click **Copy Image**.

6.  In the **Copy Image** dialog box, select **Encrypt**. Then, select a key from the drop-down list.

    By default, **Default Service CMK** is used, which indicates a service-managed CMK. You can also select a CMK that you create in KMS for encryption. The CMK that you create allows for more permissions on the data disk. In emergencies, you can disable KMS-based decryption on an ECS instance by revoking permissions or disabling CMKs.

    **Note:** If this is your first time to select a different custom encryption key, click **Confirm Authorization Policy** and select AliyunECSDiskEncryptDefaultRole to allow ECS to access your KMS resources. This step describes only how to configure the encryption settings when you copy a custom image. For more information about other settings, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).

    ![Copy Image dialog box in the ECS console](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1073559951/p75715.png)

7.  Click **OK**.


## Encrypt a data disk

You can encrypt a data disk when you create an ECS instance or create the disk.

**Encrypt a data disk when you create an ECS instance**

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  On the **Instances** page, click **Create Instance**.

4.  In the **Storage** section of the page that appears, create a data disk and configure the encryption settings.

    **Note:** This step describes only how to configure the encryption settings when you create an ECS instance. For more information about other settings, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

    1.  Click **Add Disk**.

    2.  Specify the disk category and capacity.

    3.  Select **Disk Encryption**. Then, select a key from the drop-down list.

        By default, **Default Service CMK** is used, which indicates a service-managed CMK. You can also select a CMK that you create in KMS for encryption. The CMK that you create allows for more permissions on the data disk. In emergencies, you can disable KMS-based decryption on an ECS instance by revoking permissions or disabling CMKs.

        **Note:** If this is your first time to select a different custom encryption key, click **Confirm Authorization Policy** and select AliyunECSDiskEncryptDefaultRole to allow ECS to access your KMS resources.

        ![Encrypt a data disk when you create an ECS instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0082909951/p76508.png)


**Encrypt a data disk when you create the disk**

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.

3.  In the upper-right corner of the Disks page, click **Create Disk**.

4.  Specify the disk category and capacity.

    **Note:** This step describes only how to configure the encryption settings when you create a disk. For more information about other settings, see [Create a disk](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk.md).

5.  In the **Storage** section of the page that appears, select **Disk Encryption**. Then, select a key from the drop-down list.

    By default, **Default Service CMK** is used, which indicates a service-managed CMK. You can also select a CMK that you create in KMS for encryption. The CMK that you create allows for more permissions on the data disk. In emergencies, you can disable KMS-based decryption on an ECS instance by revoking permissions or disabling CMKs.

    **Note:** If this is your first time to select a different custom encryption key, click **Confirm Authorization Policy** and select AliyunECSDiskEncryptDefaultRole to allow ECS to access your KMS resources.

    ![Create pay-as-you-go data disks](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8745721061/p4412.png)


