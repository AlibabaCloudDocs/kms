# Overview

For ApsaraDB RDS, Secrets Manager allows you to configure dynamic ApsaraDB RDS secrets that are automatically rotated on a regular basis. This reduces the security threats faced by business data.

## Background information

The attack against databases is one of the main threats to data security. To reduce the security risks of data leaks, you must effectively protect and regularly rotate secrets. When enterprises protect and rotate secrets, they may encounter the following issues:

-   To protect the plaintext of secrets, enterprises must encrypt secrets. The process of application deployment becomes longer, which brings high research and development \(R&D\) and operations and maintenance \(O&M\) costs. It is also difficult to enforce the process.
-   Lack of software facilities for automatic secret rotation. Manual secret rotation relies on the cooperation of multiple roles such as security, O&M, and R&D. A manual secret rotation process is difficult to develop and implement and is prone to errors.
-   Lack of rapid emergency response to secret leak events. System errors may occur when secret leak events are handled.
-   Lack of centralized management for the secrets required by cloud resources. As a result, large-scale management cannot be realized, and the management costs are high.

## Solution

Secrets Manager supports dynamic ApsaraDB RDS secrets. Secrets Manager encrypts dynamic ApsaraDB RDS secrets and rotates them at a high frequency. Secrets Manager provides a simple and effective method to use ApsaraDB RDS secrets and allows you to obtain enhanced security at lower R&D and O&M costs. The validity period of each secret is shortened to reduce the risks brought by data leaks in ApsaraDB RDS databases.

Dynamic ApsaraDB RDS secrets have the following benefits:

-   Prevent the leaks of static passwords of database accounts to improve data security.
-   Provide simple access methods for clients so that applications can use the secrets in a codeless or low-code way.
-   Provide emergency response capabilities. Applications are not affected when you manually rotate secrets in an one-off manner.
-   Allow you to use operation orchestration tools such as Terraform or Resource Orchestration Service \(ROS\) to manage ApsaraDB RDS resources and secrets. This meets the requirements for centralized and large-scale security management.

## Architecture

After dynamic ApsaraDB RDS secrets are used, you do not need to configure static passwords of database accounts for your applications. You can create fully managed ApsaraDB RDS secrets and set the automatic rotation period in Secrets Manager. Then, applications call the [GetSecretValue](/intl.en-US/API Reference/Secrets/GetSecretValue.md) operation to obtain the account password to access the managed ApsaraDB RDS database. The password is valid only before the next rotation.

![RDS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4882590161/p225540.png)

## Limits

Dynamic ApsaraDB RDS secrets support specific ApsaraDB RDS databases.

-   Supported databases

    ApsaraDB RDS for MySQL, ApsaraDB RDS for MariaDB TX, and ApsaraDB RDS for SQL Server except for instances that run SQL Server 2017 EE

-   Databases that are not supported

    ApsaraDB RDS for SQL Server that runs SQL Server 2017 EE, ApsaraDB RDS for PostgreSQL, and ApsaraDB RDS for PPAS


