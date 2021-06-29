# Overview

Elastic Compute Service \(ECS\) secrets store the passwords and SSH public and private keys that are used for authentication when users log on to ECS instances. Secrets Manager can periodically rotate managed ECS secrets to change ECS logon credentials among strong passwords and SSH keys. You can also manually rotate ECS secrets. This reduces the risk of ECS secret leaks.

## Benefits

Secrets Manager uses the following measures to implement **centralized and secure management** of ECS secrets:

-   **Encryption protection**: Dedicated hardware is used to encrypt ECS secrets to ensure their security in storage.
-   **Permission management**: The fine-grained permission management based on Resource Access Management \(RAM\) reduces the risk of secret leaks.
-   **Manual rotation**: When an ECS secret is leaked, you can immediately rotate the ECS secret to block intrusions.
-   **Periodic rotation**: ECS logon credentials are periodically changed to strong passwords and SSH keys. This ensures the security of ECS instances even if an undetected secret leak occurs.

## Use dynamic ECS secrets

To use dynamic ECS secrets, you must grant Secrets Manager the permissions to manage passwords and SSH keys for ECS instances, and then use Secrets Manager to manage ECS logon credentials. If a user needs to log on to an ECS instance, the user can obtain the ECS secret from Secrets Manager, and then use the ECS secret to log on to the ECS instance.

ECS secrets are rotated without manual intervention. When an automatic or manual rotation is triggered, Secrets Manager sends a secret rotation command to Cloud Assistant. Then, Cloud Assistant calls the plug-in installed on an ECS instance to complete the rotation. After the rotation, users can use the new secret to log on to the ECS instance.

![Architecture](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1752594261/p290078.png)

Use a dynamic ECS secret in the following process:

1.  [Create a dynamic ECS Secret](/intl.en-US/Secrets Manager/Dynamic ECS secrets/Manage dynamic ECS secrets.md).
2.  [Monitor the rotation of dynamic ECS secrets](/intl.en-US/Secrets Manager/Dynamic ECS secrets/Monitor the rotation of dynamic ECS secrets.md).
3.  Use the ECS secret to log on to the ECS instance.

## Limits

Linux-based ECS instances support rotation of passwords and SSH keys, whereas Windows-based ECS instances support rotation of only passwords.

