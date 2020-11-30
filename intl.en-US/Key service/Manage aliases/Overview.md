# Overview

Aliases are optional to CMKs. Aliases must be unique in a region for each Alibaba Cloud account. An Alibaba Cloud account can have identical aliases in different regions. An alias can be bound to only one CMK in a region, but a CMK can have multiple aliases.

Although aliases are bound to CMKs, aliases are resources independent of CMKs. Aliases have the following characteristics:

-   You can call the [UpdateAlias](/intl.en-US/API Reference/Key/UpdateAlias.md) operation to bind an alias to a different CMK. This operation does not affect the CMK.
-   If you delete an alias, the CMK to which the alias is bound is not deleted.
-   RAM users must be authorized before they can perform operations on an alias. For more information, see [Use RAM to control access to resources](/intl.en-US/Access control and audit/Use RAM to control access to resources.md).
-   Aliases cannot be modified. To change the alias of a CMK, you must delete the original alias and create a new one for the CMK.

You can replace the CMK ID in the request parameters for the following API operations with an alias that is bound to the CMK:

-   [DescribeKey](/intl.en-US/API Reference/Key/DescribeKey.md)
-   [Encrypt](/intl.en-US/API Reference/Key/Encrypt.md)
-   [GenerateDataKey](/intl.en-US/API Reference/Key/GenerateDataKey.md)
-   [GenerateDataKeyWithoutPlaintext](/intl.en-US/API Reference/Key/GenerateDataKeyWithoutPlaintext.md)

**Note:** To specify an alias instead of a CMK ID in the request parameters for the preceding operations, a RAM user must have the relevant permissions on the CMK. The RAM user does not need to have permissions on the alias.

An alias must contain the `alias` prefix, such as `alias/example`.

The following table describes the operations related to aliases.

|Operation|Description|
|---------|-----------|
|[t1943518.md\#]()|Create an alias to facilitate key management.|
|[t1989464.md\#]()|Bind an alias to a different CMK.|
|[t1989468.md\#]()|Query all the aliases under the current Alibaba Cloud account in the current region.|
|[Query aliases bound to a specified CMK](/intl.en-US/Key service/Manage aliases/Query aliases bound to a specified CMK.md)|Query the aliases bound to a specified CMK.|
|[t1943553.md\#]()|Delete an alias. If you delete an alias, the CMK to which the alias is bound is not deleted.|

