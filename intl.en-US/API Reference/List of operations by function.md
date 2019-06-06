# List of operations by function {#concept_vdd_rmk_xdb .concept}

This topic lists the APIs in KMS. For more information, see related documentation.

Alibaba Cloud also provides a command line tool for you to learn APIs and for the purpose of command line automation. For more information about how to install and use the command line tool, see [Alibaba Cloud CLI](https://partners-intl.aliyun.com/help/doc-detail/66653.htm)

## Key management APIs {#section_2lu_usm_ym8 .section}

Key management APIs are used to create and modify keys and manage their lifecycle.

|API|Description|
|---|-----------|
|[CreateKey](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22698_V3.html#concept_28947_zh)|Creates a CMK. You can also choose to let KMS generate key material, or upload your own key material. CreateKey is the first step to create a BYOK \(Bring Your Own Key\).|
|[GetParametersForImport](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22708_V2.html#concept_68621_zh)|Obtains the key material, which is the second step to create a BYOK.|
|[ImportKeyMaterial](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22709_V1.html#concept_68622_zh)|Imports the key material to the CMK, which is the final step to create a BYOK.|
|[EnableKey](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22705_V1.html#concept_35150_zh)|Modifies the key status to enabled.|
|[DisableKey](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22704_V1.html#concept_35151_zh)|Modifies the key status to disabled.|
|[ScheduleKeyDeletion](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22713_V1.html#concept_44196_zh)|Schedules key deletion. The key status changes to PendingDeletion. A CMK in the PendingDeletion state will be deleted when the scheduled period expires.|
|[CancelKeyDeletion](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22696_V1.html#concept_44197_zh)|Cancels the scheduled deletion of a CMK. You can cancel a scheduled deletion request after it is submitted and before the end of the scheduled period. After the scheduled deletion is canceled, the CMK returns to the enabled state.|
|[DeleteKeyMaterial](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22701_V1.html#concept_68623_zh)|Deletes the key material of a CMK. You can directly delete the key material of BYOK. After the key material is deleted, the BYOK is in the PendingImport state.|
|[DescribeKey](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22702_V3.html#concept_28952_zh)|Queries detailed information about a specified CMK.|
|[ListKeys](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22712_V2.html#concept_28951_zh)|Lists all CMKs within the current region that belong to the current Alibaba Cloud account.|

## Key operation APIs {#section_it2_2bz_0e2 .section}

Key operation APIs are used to perform data operations involving keys such as encryption and decryption.

|API|Description|
|---|-----------|
|[Encrypt](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22706_V1.html#concept_28949_zh)|Uses a specified CMK to encrypt data. The API is used for online encryption of data of no more than 6 KB.|
|[GenerateDataKey](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22707_V3.html#concept_28948_zh)|Generates a random number. After the random number is encrypted with the specified CMK, its ciphertext and plaintext are returned. The random number can be used as a data key to encrypt or decrypt a large amount of data locally.|
|[Decrypt](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22699_V3.html#concept_28950_zh)|Decrypts ciphertexts generated with the Encrypt or GenerateDataKey API. You do not need to specify the CMK for decryption.|

## Alias management APIs {#section_bwa_gxm_3z5 .section}

An alias is an independent object that must be bound to a unique CMK. Then it can be used to indicate the CMK replaced instead of KeyId.

|API|Description|
|---|-----------|
|[CreateAlias](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22697_V2.html#concept_68624_zh)|Creates an alias and binds it to a CMK.|
|[UpdateAlias](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22714_V1.html#concept_68625_zh)|Binds a specified alias to the new CMK.|
|[DeleteAlias](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22700_V1.html#concept_68626_zh)|Deletes a specified alias.|
|[ListAliases](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22710_V2.html#concept_68627_zh)|Lists all aliases of an Alibaba Cloud account in the current region.|
|[ListAliasesByKeyId](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_22711_V2.html#concept_68628_zh)|Lists all aliases bound to the specified CMK.|

## Tag management APIs {#section_vku_otz_b00 .section}

CMKs support tags. You can add multiple tags to a CMK. A tag is defined by a pair of TagKeyand TagValue.

|API|Description|
|---|-----------|
|[TagResource](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_249253_V1.html#reference_303902)|Adds or modifies the tags of a CMK.|
|[UntagResource](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_249254_V1.html#reference_303902)|Deletes the specified tag of a CMK.|
|[ListResourceTags](http://icms.alibaba-inc.com/tasks/done/translate/ZH-CN_TP_249255_V1.html#reference_303904)|Lists all tags of a CMK.|

