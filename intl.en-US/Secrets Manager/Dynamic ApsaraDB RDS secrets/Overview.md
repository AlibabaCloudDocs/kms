# Overview

Attacks against databases are one of the main threats to data security. For ApsaraDB RDS, Secrets Manager allows you to configure dynamic ApsaraDB RDS secrets that are automatically rotated on a regular basis. This reduces the security threats faced by business data.

## Architecture

After dynamic ApsaraDB RDS secrets are used, you do not need to configure static passwords of database accounts for your applications. You can create fully managed ApsaraDB RDS secrets and set the interval of automatic rotation in Secrets Manager. Then, your applications can call the [GetSecretValue](/intl.en-US/API Reference/Secrets/GetSecretValue.md) operation to obtain the account password to access the managed ApsaraDB RDS instance. The password is valid only before the next rotation.

After an ApsaraDB RDS secret is rotated, the database account and password of the RDS instance for which the secret is created are also updated. We recommend that you do not delete the RDS instance in this case. If you delete the instance, rotation of the secret may fail.

![RDS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4882590161/p225540.png)

## Limits

You can create dynamic ApsaraDB RDS secrets only for ApsaraDB RDS for MySQL, ApsaraDB RDS for MariaDB TX, ApsaraDB RDS for SQL Server, and ApsaraDB RDS for PostgreSQL instances. Note that you cannot create the secrets for RDS instances that run SQL Server 2017 EE.

## Use dynamic ApsaraDB RDS secrets

1.  [t2005680.md\#section\_tgu\_kh8\_a02](/intl.en-US/Secrets Manager/Dynamic ApsaraDB RDS secrets/Create a dynamic ApsaraDB RDS secret.md)
2.  [Monitor the rotation of dynamic ApsaraDB RDS secrets](/intl.en-US/Secrets Manager/Dynamic ApsaraDB RDS secrets/Monitor the rotation of dynamic ApsaraDB RDS secrets.md)
3.  [Allow applications to access Secrets Manager](/intl.en-US/Secrets Manager/Allow applications to access Secrets Manager.md)

