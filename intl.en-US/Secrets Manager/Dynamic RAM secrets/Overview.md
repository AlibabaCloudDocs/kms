# Overview

A Resource Access Management \(RAM\) secret stores an AccessKey pair of a RAM user, including the AccessKey ID and AccessKey secret. The AccessKey pair is used to authenticate the RAM user when the RAM user calls Alibaba Cloud APIs. Secrets Manager can regularly and automatically rotate RAM secrets to make the RAM secrets dynamic. This reduces the risks of RAM secret leaks. In addition to periodic rotation, Secrets Manager allows you to immediately rotate a RAM secret to change the AccessKey pair in use. This is useful when a RAM secret leak has occurred.

## Use dynamic RAM secrets

If you use a dynamic RAM secret in your application, no AccessKey pairs need to be configured in the application. After an administrator creates a dynamic RAM secret in Secrets Manager and configures the automatic rotation interval, your application can call the [GetSecretValue](/intl.en-US/API Reference/Secrets/GetSecretValue.md) operation to obtain a valid AccessKey pair. Then, your application can use the AccessKey pair to call Alibaba Cloud APIs.

After a dynamic RAM secret is rotated, the AccessKey pair of the RAM user associated with the secret is synchronously updated. Do not delete RAM users that are associated with dynamic RAM secrets. If you do so, the secrets fail to be rotated.

![Achitecture](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6479790261/p273787.png)

Use a dynamic RAM secret in the following process:

1.  [t2071362.md\#]().
2.  [t2071371.md\#section\_tgu\_kh8\_a02]().
3.  [Allow applications to access Secrets Manager](/intl.en-US/Secrets Manager/Allow applications to access Secrets Manager.md).
4.  Use the dynamic RAM secret to access Alibaba Cloud services.

## Limits

Secrets Manager can manage only the AccessKey pairs of RAM users, but not AccessKey pairs of Alibaba Cloud accounts.

