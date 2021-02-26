# Create a dynamic ApsaraDB RDS secret

You can create a dynamic ApsaraDB RDS secret that is automatically rotated on a regular basis. This way, the risks of data leaks can be reduced. This topic describes how to create a dynamic ApsaraDB RDS secret in the Key Management Service \(KMS\) console.

-   An ApsaraDB RDS instance is created. For more information, see [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md).
-   If a RAM user or RAM role is used to manage secrets, the system policy [AliyunKMSSecretAdminAccess](https://ram.console.aliyun.com/policies/AliyunKMSSecretAdminAccess/System/content) is attached to the RAM user or RAM role. This policy grants the following permissions:
    -   The permission to use the features of Secrets Manager.
    -   The permissions to query ApsaraDB RDS instances and manage accounts.
    -   The permission to create the service-linked role used by managed ApsaraDB RDS secrets.

## Procedure

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region where you want to create a secret.

3.  In the left-side navigation pane, click **Secrets**.

4.  Click **Create Secret**.

5.  In the Configure credentials step, set the parameters as required and click **Next**.

    1.  Set the **Secret Type** parameter to **Managed Credential for RDS**.

    2.  Enter a secret name.

    3.  Select an ApsaraDB RDS instance.

    4.  Set the secret value.

        -   **Manage Dual Account** \(recommended\): This option applies to the scenario where the accounts are used by applications to access the database. KMS hosts two accounts that have the identical permissions. This ensures that applications can still access the database at the moment when the password is reset and switched.
            -   Click the **One-click creation and authorization** tab, specify an account name, select an database, and then specify the permission.

                **Note:** KMS does not immediately create the accounts. Instead, KMS creates the accounts after you review and confirm the secret information.

            -   Click the **Import existing accounts** tab, select usernames, and then specify passwords.

                **Note:** We recommend that you specify the same passwords as that were specified for the accounts when the ApsaraDB RDS instance was created. If the imported account and password do not match, you can obtain the correct password for the account after the first rotation of the secret.

        -   **Manage Single Account**: This option applies to the scenario where high-privileged accounts or manual operations and maintenance \(O&M\) accounts are hosted. The current version of the secret may be temporarily unavailable at the moment when the password is reset and switched.
            -   Click the **One-click creation and authorization** tab, specify an account name, and then select an account type.

                You can select **Common Account** or **High Authority Account**. If you select **Common Account**, you must select a database and specify the permission.

            -   Click the **Import existing accounts** tab, select a username, and then specify the password.
    5.  Enter a description of the configuration.

6.  In the Configuration rotation step, select **Turn on automatic rotation**, set the **Rotation Period** parameter, and then click **Next**.

7.  In the Review and confirm step, review the secret configuration and rotation configuration, and click **OK**.

8.  In the Created successfully dialog box, click **Close**.

    You can also click **Secret Details** to view the secret information.


## References

-   [Allow applications to access Secrets Manager](/intl.en-US/Secrets Manager/Allow applications to access Secrets Manager.md)
-   [Use ActionTrail to query KMS event logs](/intl.en-US/Access Control and Audit/Use ActionTrail to query KMS event logs.md)
-   [Monitor the rotation of dynamic ApsaraDB RDS secrets](/intl.en-US/Secrets Manager/Dynamic ApsaraDB RDS secrets/Monitor the rotation of dynamic ApsaraDB RDS secrets.md)

