# Delete an alias

You can delete aliases that are no longer useful. If you delete an alias, the CMK to which the alias is bound is not affected.

## Background information

If you want to allow a RAM user to delete an alias, you must create a custom policy to grant the RAM user the required permissions.

The following example shows the content of a policy that allows user 123456 to delete the `alias/example` alias that is bound to CMK 127d2f84-ee5f-4f4d-9d41-dbc1aca2\*\*\*\*:

```
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
```

## Delete an alias in the KMS console

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the top navigation bar, select the region where your CMK resides.

3.  In the left-side navigation pane, click **Keys**.

4.  Find the CMK and click the alias in the **Alias Name** column.

5.  On the page that appears, find the alias that you want to delete in the **Aliases** section and click **Delete Alias**.

6.  In the Delete Alias message, click **OK**.


## Delete an alias by calling an API operation

Call the [DeleteAlias](/intl.en-US/API Reference/Key/DeleteAlias.md) operation to delete an alias.

## Delete an alias by running a command on the Alibaba Cloud CLI

Run the aliyun kms DeleteAlias command to delete an alias.

```
aliyun kms DeleteAlias --AliasName alias/example
```

