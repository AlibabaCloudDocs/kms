# API 概览 {#concept_vdd_rmk_xdb .concept}

本文列举了密钥管理服务（KMS）提供的 API 接口，具体 API 接口信息请参考相关文档。

阿里云也提供命令行工具，供您学习 API 或用于命令行自动化。关于命令行工具的安装和使用，详情请参考：[阿里云 CLI](https://www.alibabacloud.com/help/doc-detail/66653.htm)。

## 密钥管理接口 {#section_i54_gmj_3gb .section}

密钥管理接口用于密钥的创建、属性修改以及生命周期管理。

|API|描述|
|:--|:-|
|[CreateKey](intl.zh-CN/API 参考/API列表/CreateKey.md#)|创建用户主密钥。用户可以选择由 KMS 生成密钥材料；也可以选择自己上传密钥材料（也就是BYOK，此时CreateKey是 BYOK 的第一步）。|
|[GetParametersForImport](intl.zh-CN/API 参考/API列表/GetParametersForImport.md#)|创建外部密钥（BYOK）的第二步：获取导入主密钥的材料。|
|[ImportKeyMaterial](intl.zh-CN/API 参考/API列表/ImportKeyMaterial.md#)|创建外部密钥（BYOK）的第三步：导入密钥材料到用户主密钥中，完成外部密钥的创建。|
|[EnableKey](intl.zh-CN/API 参考/API列表/EnableKey.md#)|修改密钥的状态为：启用。|
|[DisableKey](intl.zh-CN/API 参考/API列表/DisableKey.md#)|修改密钥的状态为：禁用。|
|[ScheduleKeyDeletion](intl.zh-CN/API 参考/API列表/ScheduleKeyDeletion.md#)|计划删除密钥。将密钥的状态设置为待删除状态，处于待删除状态的主密钥，会在计划的日期到期后删除。|
|[CancelKeyDeletion](intl.zh-CN/API 参考/API列表/CancelKeyDeletion.md#)|取消计划删除。处于待删除状态的密钥，在计划的日期到期之前，可以取消删除的计划，重新设置密钥状态为：启用。|
|[DeleteKeyMaterial](intl.zh-CN/API 参考/API列表/DeleteKeyMaterial.md#)|直接删除用户主密钥的密钥材料。针对导入的外部密钥（BYOK），可以直接删除导入的密钥材料，删除密钥材料后的用户主密钥状态为：等待导入。|
|[DescribeKey](intl.zh-CN/API 参考/API列表/DescribeKey.md#)|查询指定密钥的信息。|
|[ListKeys](intl.zh-CN/API 参考/API列表/ListKeys.md#)|列出云帐号在本地域的所有密钥。|

## 密码运算接口 {#section_bmq_3mj_3gb .section}

密码运算接口用于对数据进行密码运算，例如：数据的加密和解密。

|API|描述|
|:--|:-|
|[Encrypt](intl.zh-CN/API 参考/API列表/Encrypt.md#)|使用指定用户主密钥加密数据，用于少量数据（不多于6KB）的在线加密。|
|[GenerateDataKey](intl.zh-CN/API 参考/API列表/GenerateDataKey.md#)|产生一个随机数，并用指定的用户主密钥加密后，返回随机数的密文以及明文。随机数可被用作数据密钥，在本地做大量数据加密或解密。|
|[Decrypt](intl.zh-CN/API 参考/API列表/Decrypt.md#)|解密 Encrypt 或 GenerateDataKey接口产生的密文，不需要指定用于解密的用户主密钥。|

## 别名管理接口 {#section_dcl_lmj_3gb .section}

别名是独立的对象，但是必须和唯一的用户主密钥进行绑定，从而可以在特定 API 中代替 KeyId 参数来指代用户主密钥。

|API|描述|
|:--|:-|
|[CreateAlias](intl.zh-CN/API 参考/API列表/CreateAlias.md#)|创建一个别名，并且将别名与一个用户主密钥绑定。|
|[UpdateAlias](intl.zh-CN/API 参考/API列表/UpdateAlias.md#)|绑定指定别名到新的用户主密钥。|
|[DeleteAlias](intl.zh-CN/API 参考/API列表/DeleteAlias.md#)|删除指定别名。|
|[ListAliases](intl.zh-CN/API 参考/API列表/ListAliases.md#)|列出云帐号在本地域的所有别名。|
|[ListAliasesByKeyId](intl.zh-CN/API 参考/API列表/ListAliasesByKeyId.md#)|列出与指定用户主密钥绑定的别名。|

## 标签管理接口 {#section_hb4_mmj_3gb .section}

用户主密钥支持标签。用户可以为用户主密钥添加多个标签，每一个标签为一组标签键（TagKey）和标签值（TagValue）。

|API|描述|
|:--|:-|
|[TagResource](intl.zh-CN/API 参考/API列表/TagResource.md#)|为用户主密钥添加或修改标签。|
|[UntagResource](intl.zh-CN/API 参考/API列表/UntagResource.md#)|删除用户主密钥的指定标签。|
|[ListResourceTags](intl.zh-CN/API 参考/API列表/ListResourceTags.md#)|列出用户主密钥的所有标签。|

