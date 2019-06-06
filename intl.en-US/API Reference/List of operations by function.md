# List of operations by function {#concept_vdd_rmk_xdb .concept}

This topic lists the APIs in KMS. For more information, see related documentation.

Alibaba Cloud also provides a command line tool for you to learn APIs and for the purpose of command line automation. For more information about how to install and use the command line tool, see [Alibaba Cloud CLI](https://partners-intl.aliyun.com/help/doc-detail/66653.htm)

## Key management APIs {#section_2lu_usm_ym8 .section}

Key management APIs are used to create and modify keys and manage their lifecycle.

|API|Description|
|---|-----------|
|[CreateKey](reseller.en-US/API Reference/API list/CreateKey.md#)|Creates a CMK. You can also choose to let KMS generate key material, or upload your own key material. CreateKey is the first step to create a BYOK \(Bring Your Own Key\).|
|[GetParametersForImport](reseller.en-US/API Reference/API list/GetParametersForImport.md#)|Obtains the key material, which is the second step to create a BYOK.|
|[ImportKeyMaterial](reseller.en-US/API Reference/API list/ImportKeyMaterial.md#)|Imports the key material to the CMK, which is the final step to create a BYOK.|
|[EnableKey](reseller.en-US/API Reference/API list/EnableKey.md#)|Modifies the key status to enabled.|
|[DisableKey](reseller.en-US/API Reference/API list/DisableKey.md#)|Modifies the key status to disabled.|
|[ScheduleKeyDeletion](reseller.en-US/API Reference/API list/ScheduleKeyDeletion.md#)|Schedules key deletion. The key status changes to PendingDeletion. A CMK in the PendingDeletion state will be deleted when the scheduled period expires.|
|[CancelKeyDeletion](reseller.en-US/API Reference/API list/CancelKeyDeletion.md#)|Cancels the scheduled deletion of a CMK. You can cancel a scheduled deletion request after it is submitted and before the end of the scheduled period. After the scheduled deletion is canceled, the CMK returns to the enabled state.|
|[DeleteKeyMaterial](reseller.en-US/API Reference/API list/DeleteKeyMaterial.md#)|Deletes the key material of a CMK. You can directly delete the key material of BYOK. After the key material is deleted, the BYOK is in the PendingImport state.|
|[DescribeKey](reseller.en-US/API Reference/API list/DescribeKey.md#)|Queries detailed information about a specified CMK.|
|[ListKeys](reseller.en-US/API Reference/API list/ListKeys.md#)|Lists all CMKs within the current region that belong to the current Alibaba Cloud account.|

## Key operation APIs {#section_it2_2bz_0e2 .section}

Key operation APIs are used to perform data operations involving keys such as encryption and decryption.

|API|Description|
|---|-----------|
|[Encrypt](reseller.en-US/API Reference/API list/Encrypt.md#)|Uses a specified CMK to encrypt data. The API is used for online encryption of data of no more than 6 KB.|
|[GenerateDataKey](reseller.en-US/API Reference/API list/GenerateDataKey.md#)|Generates a random number. After the random number is encrypted with the specified CMK, its ciphertext and plaintext are returned. The random number can be used as a data key to encrypt or decrypt a large amount of data locally.|
|[Decrypt](reseller.en-US/API Reference/API list/Decrypt.md#)|Decrypts ciphertexts generated with the Encrypt or GenerateDataKey API. You do not need to specify the CMK for decryption.|

## Alias management APIs {#section_bwa_gxm_3z5 .section}

An alias is an independent object that must be bound to a unique CMK. Then it can be used to indicate the CMK replaced instead of KeyId.

|API|Description|
|---|-----------|
|[CreateAlias](reseller.en-US/API Reference/API list/CreateAlias.md#)|Creates an alias and binds it to a CMK.|
|[UpdateAlias](reseller.en-US/API Reference/API list/UpdateAlias.md#)|Binds a specified alias to the new CMK.|
|[DeleteAlias](reseller.en-US/API Reference/API list/DeleteAlias.md#)|Deletes a specified alias.|
|[ListAliases](reseller.en-US/API Reference/API list/ListAliases.md#)|Lists all aliases of an Alibaba Cloud account in the current region.|
|[ListAliasesByKeyId](reseller.en-US/API Reference/API list/ListAliasesByKeyId.md#)|Lists all aliases bound to the specified CMK.|

## Tag management APIs {#section_vku_otz_b00 .section}

CMKs support tags. You can add multiple tags to a CMK. A tag is defined by a pair of TagKeyand TagValue.

|API|Description|
|---|-----------|
|[TagResource](reseller.en-US/API Reference/API list/TagResource.md#)|Adds or modifies the tags of a CMK.|
|[UntagResource](reseller.en-US/API Reference/API list/UntagResource.md#)|Deletes the specified tag of a CMK.|
|[ListResourceTags](reseller.en-US/API Reference/API list/ListResourceTags.md#)|Lists all tags of a CMK.|

