# Bind an alias to a different CMK

This topic describes how to bind an existing alias to a different CMK.

## Background information

If you want to allow a RAM user to bind an existing alias to a different CMK, you must create a custom policy to grant the RAM user the required permissions on the original CMK, new CMK, and alias.

The following code shows the content of a custom policy that allows RAM user 123456 to bind `alias/example` to 127d2f84-ee5f-4f4d-9d41-dbc1aca2\*\*\*\*. The original CMK to which this alias is bound is 08ec3bb9-034f-485b-b1cd-3459baa8\*\*\*\*.

```
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
```

## Use an API operation

You can call the [UpdateAlias](/intl.en-US/API Reference/Key/UpdateAlias.md) operation to bind an alias to a different CMK.

## Run a command on the Alibaba Cloud CLI

Run the aliyun kms UpdateAlias command to bind an alias to a different CMK.

```
aliyun kms UpdateAlias --AliasName alias/example --KeyId 127d2f84-ee5f-4f4d-9d41-dbc1aca2****
```

