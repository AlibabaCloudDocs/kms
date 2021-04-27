# Overview

Secrets Manager allows you to manage your secrets throughout their lifecycle. Applications can access Secrets Manager by using secure and convenient methods. This prevents the risk of sensitive data leaks caused by hardcoded secrets.

## Benefits

The leaks of secrets, such as passwords of database accounts, passwords of server accounts, SSH keys, and AccessKey secrets, are one of the main threats to data security. To reduce the security risks of data leaks, you must effectively protect and regularly rotate secrets. When enterprises protect and rotate secrets, they may encounter the following issues:

-   To protect secrets, enterprises must encrypt them. The process of application deployment becomes longer, which brings high research and development \(R&D\) and operations and maintenance \(O&M\) costs. It is also difficult to enforce the process.
-   Lack of software facilities for automatic secret rotation. Manual secret rotation relies on the cooperation of multiple roles such as security, O&M, and R&D. A manual secret rotation process is difficult to develop and implement and is prone to errors.
-   Lack of rapid emergency response to secret leak events. System errors may occur when secret leak events are handled.
-   Lack of centralized management for the secrets required by cloud resources. As a result, large-scale management cannot be realized, and the management costs are high.

Secrets Manager has the following security benefits:

-   Encrypts and manages secrets to prevent the leaks of valuable assets caused by hardcoded secrets. This improves data security.
-   Provides secure and convenient access methods for clients so that applications can use the secrets in a codeless or low-code way.
-   Provides emergency response capabilities. Applications are not affected when you manually rotate secrets in a one-off manner.
-   Allows you to rotate dynamic secrets at a high frequency. This shortens the validity period of each secret and further mitigates the risks caused by secret leaks.
-   Allows you to use API operations and operation orchestration tools such as Terraform and Resource Orchestration Service \(ROS\). This meets the requirements for centralized and large-scale security management.

## Scenarios

This section uses a database username and its password as the managed secret.

![Basic](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2243949161/p268680.png)

1.  A system administrator configures a username and its password in a database, which are used to access the database from the application MyApp.
2.  The administrator creates a secret object MyDbCreds in Secrets Manager to store the username and password.
3.  When MyApp needs to access the database, it sends a request for MyDbCreds to Secrets Manager.
4.  Secrets Manager reads the username and password in ciphertext, decrypts them, and then returns the plaintext to MyApp by using HTTPS.
5.  MyApp reads and parses the plaintext returned by Secrets Manager to obtain the username and password and then uses them to access the database.

In this process, MyApp calls an API operation of Secrets Manager to obtain the username and password. This prevents the risks of data leaks caused by hardcoded secrets. The following figure shows the differences between hardcoding secrets and calling API operations of Secrets Manager.

![Secret1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2243949161/p268683.png)

## Features

-   Secret encryption: Secrets Manager uses customer master keys \(CMKs\) in Key Management Service \(KMS\) to encrypt secrets. You can specify a CMK or use the CMK that is automatically created by Secrets Manager. Secrets Manager generates an independent CMK for each Alibaba Cloud account in a region. This CMK is used for secret encryption if you do not specify the CMK to use.
-   Dynamic secret use: You applications can dynamically read secrets by using Secrets Manager Client and use the latest secret.
-   Automatic secret rotation: Secrets Manager supports out-of-the-box automatic rotation for secrets of specific types. You can also rotate secrets on a custom schedule by using Function Compute.
-   Secret access control and use auditing: You can use Resource Access Management \(RAM\) to control access to secrets. You can also use ActionTrail to audit operations such as rotating and reading secrets.

## Use Secrets Manager

Secrets Manager is used for security management and application development and deployment.

-   Security management

    Select an appropriate secret type based on your scenario. Create, manage, and rotate secrets.

    -   Passwords of ApsaraDB RDS database accounts: [Overview](/intl.en-US/Secrets Manager/Dynamic ApsaraDB RDS secrets/Overview.md).
    -   Generic secrets: [Overview](/intl.en-US/Secrets Manager/Generic Secrets/Overview.md).
-   Application development and deployment

    Applications can access Secrets Manager by using multiple methods such as KMS SDK, Secrets Manager Client, and the Kubernetes plug-in. Applications can dynamically read sensitive secret values based on the secret name. For more information, see [Allow applications to access Secrets Manager](/intl.en-US/Secrets Manager/Allow applications to access Secrets Manager.md).


