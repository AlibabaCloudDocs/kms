# Create an alias

Aliases are optional to customer master keys \(CMKs\). You can create aliases to facilitate CMK management.

-   An alias must contain the `alias/` prefix. An alias name excluding the prefix must be 1 to 255 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and forward slashes \(/\).
-   If you want to allow a Resource Access Management \(RAM\) user to create an alias, you must create a custom policy to grant the RAM user the required permissions.

    The following sample policy allows User 123456 to create an alias named `alias/example` for CMK 08ec3bb9-034f-485b-b1cd-3459baa8\*\*\*\*:

    ```
    {
      "Version": "1",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "kms:CreateAlias"
          ],
          "Resource": [
            "acs:kms:cn-hangzhou:123456:key/08ec3bb9-034f-485b-b1cd-3459baa8****",
            "acs:kms:cn-hangzhou:123456:alias/example"
          ]
        }
      ]
    }
    ```

-   A new alias created for a CMK does not affect the existing aliases of the CMK.

## Create an alias in the KMS console

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the top navigation bar, select the region where your CMK resides.

3.  In the left-side navigation pane, click **Keys**.

4.  Find the CMK for which you want to create an alias and click **Create Alias** below the CMK ID in the **Key** column.

5.  In the Create Alias dialog box, specify Alias Name.

6.  Click **OK**.

    **Note:** If you want to create more aliases for the CMK, click the ID of the CMK. In the **Aliases** section of the page that appears, click **Create Alias**.


## Create an alias by calling an API operation

Call the [t22697.md\#](/intl.en-US/API Reference/Key/CreateAlias.md) operation to create an alias.

## Create an alias by running a command in Alibaba Cloud CLI

Run the aliyun kms CreateAlias command to create an alias.

```
aliyun kms CreateAlias --KeyId 08ec3bb9-034f-485b-b1cd-3459baa8**** --AliasName alias/example
```

