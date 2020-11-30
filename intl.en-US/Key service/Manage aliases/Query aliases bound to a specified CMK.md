# Query aliases bound to a specified CMK

When you query the aliases bound to a specified CMK, only the related aliases are returned.

## Background information

To allow a RAM user to query the aliases bound to a specified CMK, you must create custom policies and assign the policies to the RAM user.

For example, User 123456 queries the aliases bound to the CMK 127d2f84-ee5f-4f4d-9d41-dbc1aca2\*\*\*\*. The following code shows the RAM policy:

```
{
  "Version": "1",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "kms:ListAliasesByKeyId"
      ],
      "Resource": [
        "acs:kms:cn-hangzhou:123456:key/127d2f84-ee5f-4f4d-9d41-dbc1aca2****"
      ]
    }
  ]
}
```

## Query the aliases bound to a specified CMK by calling an API operation

You can call the [ListAliasesByKeyId](/intl.en-US/API Reference/Key/ListAliasesByKeyId.md) operation to query the aliases bound to a specified CMK.

## Query the aliases bound to a specified CMK by using Alibaba Cloud CLI

You can run the aliyun kms ListAliasesByKeyId command to query the aliases bound to a specified CMK.

```
aliyun kms ListAliasesByKeyId --KeyId 127d2f84-ee5f-4f4d-9d41-dbc1aca2****
```

