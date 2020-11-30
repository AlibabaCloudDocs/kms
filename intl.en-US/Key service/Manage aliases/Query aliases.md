# Query aliases

You can query all aliases under your Alibaba Cloud account in the current region.

## Background information

If you want to allow a RAM user to query aliases, you must create a custom policy to grant the RAM user the required permissions.

The following example shows the content of a policy that allows user 123456 to query aliases:

```
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
```

## Query aliases by calling an API operation

Call the [ListAliases](/intl.en-US/API Reference/Key/ListAliases.md) operation to query aliases.

## Query aliases by running a command on the Alibaba Cloud CLI

Run the aliyun kms ListAliases command to query aliases.

```
aliyun kms ListAliases
```

