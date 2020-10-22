# API概览

本文列出了密钥管理服务KMS（Key Management Service）提供的API接口及相关描述。

阿里云也提供了命令行工具，供您学习API或用于自动化执行命令行。关于命令行工具的安装和使用，请参见[阿里云CLI](https://help.aliyun.com/document_detail/66653.html)。

## 密钥服务接口

-   **用户主密钥管理**

    密钥管理接口用于密钥的创建、属性修改以及生命周期管理。

    |API|描述|
    |:--|:-|
    |[CreateKey](/cn.zh-CN/API参考/密钥/CreateKey.md)|创建用户主密钥。用户可以选择由KMS生成密钥材料，也可以选择自己上传密钥材料（即是BYOK，此时CreateKey是BYOK的第一步）。|
    |[GetParametersForImport](/cn.zh-CN/API参考/密钥/GetParametersForImport.md)|创建外部密钥（BYOK）的第二步：获取导入主密钥的材料。|
    |[ImportKeyMaterial](/cn.zh-CN/API参考/密钥/ImportKeyMaterial.md)|创建外部密钥（BYOK）的第三步：导入密钥材料到用户主密钥中，完成外部密钥的创建。|
    |[EnableKey](/cn.zh-CN/API参考/密钥/EnableKey.md)|修改密钥的状态为启用。|
    |[DisableKey](/cn.zh-CN/API参考/密钥/DisableKey.md)|修改密钥的状态为禁用。|
    |[ScheduleKeyDeletion](/cn.zh-CN/API参考/密钥/ScheduleKeyDeletion.md)|计划删除密钥。将密钥的状态设置为待删除状态，处于待删除状态的主密钥，会在计划日期到期后删除。|
    |[CancelKeyDeletion](/cn.zh-CN/API参考/密钥/CancelKeyDeletion.md)|取消计划删除。处于待删除状态的密钥，在计划的日期到期之前，可以取消删除的计划，重新设置密钥状态为启用。|
    |[DeleteKeyMaterial](/cn.zh-CN/API参考/密钥/DeleteKeyMaterial.md)|直接删除用户主密钥的密钥材料。针对导入的外部密钥（BYOK），可以直接删除导入的密钥材料，删除密钥材料后的用户主密钥状态为等待导入。|
    |[DescribeKey](/cn.zh-CN/API参考/密钥/DescribeKey.md)|查询指定密钥的信息。|
    |[ListKeys](/cn.zh-CN/API参考/密钥/ListKeys.md)|列出云账号在本地域的所有密钥。|
    |[UpdateKeyDescription](/cn.zh-CN/API参考/密钥/UpdateKeyDescription.md)|更新用户主密钥的描述信息。|

-   **密钥版本管理**

    密钥版本管理接口用于对主密钥进行密钥轮转。

    |API|描述|
    |---|--|
    |[DescribeKeyVersion](/cn.zh-CN/API参考/密钥/DescribeKeyVersion.md)|查看一个密钥版本。|
    |[ListKeyVersions](/cn.zh-CN/API参考/密钥/ListKeyVersions.md)|列出主密钥的所有密钥版本。|
    |[UpdateRotationPolicy](/cn.zh-CN/API参考/密钥/UpdateRotationPolicy.md)|更新对称主密钥的轮转策略。如果配置自动轮转，KMS将周期性自动生成新的密钥版本。|
    |[CreateKeyVersion](/cn.zh-CN/API参考/密钥/CreateKeyVersion.md)|创建新的密钥版本，适用于非对称密钥。|

-   **密码运算**

    密码运算接口用于对数据进行密码运算，例如数据的加密和解密。

    |API|描述|
    |:--|:-|
    |[Encrypt](/cn.zh-CN/API参考/密钥/Encrypt.md)|使用指定用户主密钥加密数据，用于少量数据（不多于6KB）的在线加密。|
    |[GenerateDataKey](/cn.zh-CN/API参考/密钥/GenerateDataKey.md)|产生一个随机数，并用指定的用户主密钥加密后，返回随机数的密文以及明文。随机数可被用作数据密钥，在本地做大量数据加密或解密。|
    |[GenerateDataKeyWithoutPlaintext](/cn.zh-CN/API参考/密钥/GenerateDataKeyWithoutPlaintext.md)|产生一个随机数，并用指定的用户主密钥加密后，返回随机数的密文。随机数可被用作数据密钥，在本地做大量数据加密或解密。|
    |[ExportDataKey](/cn.zh-CN/API参考/密钥/ExportDataKey.md)|使用传入的公钥加密导出数据密钥。|
    |[GenerateAndExportDataKey](/cn.zh-CN/API参考/密钥/GenerateAndExportDataKey.md)|随机生成一个数据密钥，通过您指定的主密钥（CMK）和公钥加密后，返回CMK加密数据密钥的密文和公钥加密数据密钥的密文。|
    |[Decrypt](/cn.zh-CN/API参考/密钥/Decrypt.md)|解密Encrypt或GenerateDataKey接口产生的密文，不需要指定用于解密的用户主密钥。|
    |[ReEncrypt](/cn.zh-CN/API参考/密钥/ReEncrypt.md)|对密文进行转加密。即先解密密文，然后将解密得到的数据或者数据密钥使用新的主密钥再次进行加密，返回加密结果。|
    |[AsymmetricSign](/cn.zh-CN/API参考/密钥/AsymmetricSign.md)|非对称密钥的私钥运算：产生数字签名。|
    |[AsymmetricVerify](/cn.zh-CN/API参考/密钥/AsymmetricVerify.md)|非对称密钥的公钥运算：验证私钥产生的数字签名。|
    |[AsymmetricDecrypt](/cn.zh-CN/API参考/密钥/AsymmetricDecrypt.md)|非对称密钥的私钥运算：解密公钥加密的数据。|
    |[AsymmetricEncrypt](/cn.zh-CN/API参考/密钥/AsymmetricEncrypt.md)|非对称密钥的公钥运算：加密数据。|
    |[GetPublicKey](/cn.zh-CN/API参考/密钥/GetPublicKey.md)|获取非对称密钥的公钥，可用于离线验证数字签名，或者加密数据。|

-   **别名管理**

    别名是独立的对象，但是必须和唯一的用户主密钥进行绑定，从而可以在特定API中代替KeyId参数来指代用户主密钥。

    |API|描述|
    |:--|:-|
    |[CreateAlias](/cn.zh-CN/API参考/密钥/CreateAlias.md)|创建一个别名，并且将别名与一个用户主密钥绑定。|
    |[UpdateAlias](/cn.zh-CN/API参考/密钥/UpdateAlias.md)|更新已存在的别名所代表的主密钥（CMK）ID。|
    |[DeleteAlias](/cn.zh-CN/API参考/密钥/DeleteAlias.md)|删除别名。|
    |[ListAliases](/cn.zh-CN/API参考/密钥/ListAliases.md)|列出云账号在本地域的所有别名。|
    |[ListAliasesByKeyId](/cn.zh-CN/API参考/密钥/ListAliasesByKeyId.md)|列出与指定用户主密钥绑定的别名。|


## 凭据管家接口

KMS凭据管家提供凭据的托管、保护、分发和轮转能力。

|API|描述|
|---|--|
|[CreateSecret](/cn.zh-CN/API参考/凭据/CreateSecret.md)|创建凭据，并存入凭据的初始版本。|
|[ListSecrets](/cn.zh-CN/API参考/凭据/ListSecrets.md)|查询当前用户云账号所在地域的所有凭据。|
|[DeleteSecret](/cn.zh-CN/API参考/凭据/DeleteSecret.md)|删除凭据对象。|
|[DescribeSecret](/cn.zh-CN/API参考/凭据/DescribeSecret.md)|获取凭据的元数据信息。|
|[GetSecretValue](/cn.zh-CN/API参考/凭据/GetSecretValue.md)|获取凭据值。|
|[PutSecretValue](/cn.zh-CN/API参考/凭据/PutSecretValue.md)|为凭据存入一个新版本的凭据值。|
|[UpdateSecret](/cn.zh-CN/API参考/凭据/UpdateSecret.md)|更新凭据的元数据。|
|[UpdateSecretVersionStage](/cn.zh-CN/API参考/凭据/UpdateSecretVersionStage.md)|更新凭据的版本状态。|
|[RestoreSecret](/cn.zh-CN/API参考/凭据/RestoreSecret.md)|恢复被删除的凭据。|
|[ListSecretVersionIds](/cn.zh-CN/API参考/凭据/ListSecretVersionIds.md)|查询凭据的所有版本信息。|
|[GetRandomPassword](/cn.zh-CN/API参考/凭据/GetRandomPassword.md)|获得一个随机密码串。|

## 标签管理接口

用户主密钥支持标签。您可以为用户主密钥添加多个标签，每一个标签为一组标签键（TagKey）和标签值（TagValue）。

|API|描述|
|:--|:-|
|[TagResource](/cn.zh-CN/API参考/标签/TagResource.md)|为用户主密钥或者凭据添加或修改标签。|
|[UntagResource](/cn.zh-CN/API参考/标签/UntagResource.md)|删除用户主密钥或者凭据的指定标签。|
|[ListResourceTags](/cn.zh-CN/API参考/标签/ListResourceTags.md)|列出用户主密钥或者凭据的所有标签。|

## 其他

|API|描述|
|:--|:-|
|[DescribeRegions](/cn.zh-CN/API参考/其他/DescribeRegions.md)|查询当前账户的可用地域列表。|
|[OpenKmsService](/cn.zh-CN/API参考/其他/OpenKmsService.md)|为当前阿里云账号开通密钥管理服务。|
|[DescribeAccountKmsStatus](/cn.zh-CN/API参考/其他/DescribeAccountKmsStatus.md)|查询当前阿里云账号的密钥管理服务状态。|

