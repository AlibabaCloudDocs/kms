# Use aliases

Aliases are optional to CMKs.

Aliases must be unique in a region for each Alibaba Cloud account. An Alibaba Cloud account can have identical aliases in different regions. An alias can be bound to only one CMK in a region, but a CMK can have multiple aliases.

Although aliases are bound to CMKs, aliases are resources independent of CMKs. Aliases have the following characteristics:

-   You can call the [t22714.md\#](/intl.en-US/API Reference/Key/UpdateAlias.md) operation to bind an alias to a different CMK. This operation does not affect the CMK.
-   If you delete an alias, the CMK to which the alias is bound is not deleted.
-   RAM users must be authorized before they can perform operations on an alias. For more information, see [Use RAM to control access to resources](/intl.en-US/Access control and audit/Use RAM to control access to resources.md).
-   Aliases cannot be modified. To change the alias of a CMK, you must delete the old alias and create a new one for the CMK.

You can replace the CMK ID in the request parameters for the following API operations with an alias that is bound to the CMK:

-   DescribeKey
-   Encrypt
-   GenerateDataKey
-   GenerateDataKeyWithoutPlaintext

To specify an alias instead of a CMK ID in the request parameters for the preceding operations, a RAM user must have the relevant permissions on the CMK. The RAM user does not need to have permissions on the alias.

You can perform the following alias-related operations:

-   [Create an alias](#section_68522_01)
-   [Bind an alias to a different CMK](#section_68522_02)
-   [Delete an alias](#section_68522_03)
-   [Obtain all aliases](#section_68522_04)
-   [Obtain the aliases that are bound to a specific CMK](#section_68522_05)

When you use an alias, you must make sure that the alias is complete. Example:

```
//A complete alias must have the alias/ prefix.
alias/example
```

## Create an alias

-   An alias must contain the `alias/` prefix. An alias \(excluding the prefix\) can contain letters, digits, underscores \(\_\), hyphens \(-\), and forward slashes \(/\). An alias \(excluding the prefix\) must be 1 to 255 characters in length.
-   To create an alias, a RAM user must have permissions on both the alias and the CMK to which the alias is bound.
-   Creating a new alias for a CMK does not affect the existing aliases of the CMK.
-   You can call the [t22697.md\#](/intl.en-US/API Reference/Key/CreateAlias.md) operation to create an alias.

```
//Grant RAM user 123456 the permissions to create the alias/example alias for the 08ec3bb9-034f-485b-b1cd-3459baa8**** CMK.
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

//Create an alias.
aliyun kms CreateAlias --KeyId 08ec3bb9-034f-485b-b1cd-3459baa8**** --AliasName alias/example
```

## Bind an alias to a different CMK

-   You can call the [t22714.md\#](/intl.en-US/API Reference/Key/UpdateAlias.md) operation to bind an existing alias to a different CMK.
-   To bind an alias to a different CMK, a RAM user must have permissions on the alias, the CMK to which the alias is currently bound, and the CMK to which you want to bind the alias.

```
//Grant RAM user 123456 the permissions to bind the alias/example alias to the 127d2f84-ee5f-4f4d-9d41-dbc1aca28788 CMK. The alias is originally bound to the 08ec3bb9-034f-485b-b1cd-3459baa8**** CMK.
{
  "Version": "1",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "kms:UpdateAlias"
      ],
      "Resource": [
        "acs:kms:cn-hangzhou:123456:key/08ec3bb9-034f-485b-b1cd-3459baa8****",
        "acs:kms:cn-hangzhou:123456:key/127d2f84-ee5f-4f4d-9d41-dbc1aca2****",
        "acs:kms:cn-hangzhou:123456:alias/example"
      ]
    }
  ]
}

//Bind an alias to a different CMK.
aliyun kms UpdateAlias --AliasName alias/example --KeyId 127d2f84-ee5f-4f4d-9d41-dbc1aca2****
```

## Delete an alias

-   You can call the [t22700.md\#](/intl.en-US/API Reference/Key/DeleteAlias.md) operation to delete an alias. Deleting an alias does not affect the CMK to which the alias is bound.
-   To delete an alias, a RAM user must have permissions on both the alias and the CMK to which the alias is bound.

```
//Grant RAM user 123456 the permissions to delete the alias/example alias of the 127d2f84-ee5f-4f4d-9d41-dbc1aca2**** CMK.
{
  "Version": "1",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "kms:DeleteAlias"
      ],
      "Resource": [
        "acs:kms:cn-hangzhou:123456:key/127d2f84-ee5f-4f4d-9d41-dbc1aca2****",
        "acs:kms:cn-hangzhou:123456:alias/example"
      ]
    }
  ]
}

//Delete an alias.
aliyun kms DeleteAlias --AliasName alias/example
```

## Obtain all aliases

-   You can call the [ListAliases](/intl.en-US/API Reference/Key/ListAliases.md) operation to obtain all aliases under your Alibaba Cloud account in the current region.
-   To obtain all aliases, a RAM user must have permissions on alias resources.

```
//Grant RAM user 123456 the permissions to obtain all aliases.
{
  "Version": "1",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "kms:ListeAliases"
      ],
      "Resource": [
        "acs:kms:cn-hangzhou:123456:alias"
      ]
    }
  ]
}

//Obtain all aliases.
aliyun kms ListAliases
```

## Obtain the aliases that are bound to a specific CMK

-   You can call the [ListAliasesByKeyId](/intl.en-US/API Reference/Key/ListAliasesByKeyId.md) operation to obtain all aliases bound to a specific CMK.
-   To obtain the aliases bound to a specific CMK, a RAM user must have permissions on the CMK.

```
//Grant RAM user 123456 the permissions to obtain all aliases bound to the 127d2f84-ee5f-4f4d-9d41-dbc1aca2**** CMK.
{
  "Version": "1",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "kms:DeleteAlias"
      ],
      "Resource": [
        "acs:kms:cn-hangzhou:123456:key/127d2f84-ee5f-4f4d-9d41-dbc1aca2****"
      ]
    }
  ]
}

//Obtain the aliases that are bound to a specific CMK.
aliyun kms ListAliasesByKeyId --KeyId 127d2f84-ee5f-4f4d-9d41-dbc1aca2****
```

