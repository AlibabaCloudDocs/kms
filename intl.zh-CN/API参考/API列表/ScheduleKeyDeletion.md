# ScheduleKeyDeletion {#concept_44196_zh .concept}

申请删除一个指定的主密钥（CMK\)。

-   在密钥预删除期间，密钥状态处于**待删除**，无法用于加密、解密、产生数据密钥操作。
-   主密钥一旦被删除无法恢复，使用该主密钥加密的内容与使用该主密钥产生的数据密钥（Datakey）均无法再被解密。因此，我们不提供直接删除主密钥的功能，而是采用申请删除的方式。并且我们建议您尽可能选择密钥禁用[DisableKey](intl.zh-CN/API 参考/API列表/DisableKey.md#)。
-   在申请删除主密钥的同时，需要指定一个预删除周期，该周期最少为 7 天，最多为 30 天。从申请删除主密钥的时刻开始，到删除周期之前，可以通过[CancelKeyDeletion](intl.zh-CN/API 参考/API列表/CancelKeyDeletion.md#)撤销密钥删除的申请。
-   密钥会在到达预删除时间后的 24 小时之内被删除。API 服务器采用 UTC 时间。 例如用户 A 在2016年9月10日14:00申请了一个主密钥删除，预计删除时间在 7 天以后，那么KMS服务将在9月17日14:00之后的 24 小时内完成删除。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|CMK 全局唯一标识符。|
|PendingWindowInDays|Integer|是|密钥预删除周期。在这段时间内，您可以撤销删除处于**待删除**状态的密钥；预删除时间过后无法撤销删除。有效值：最小值为 7，最大值为 30。|

## 返回参数 { .section}

|名称|类型|描述|
|RequestId|String|本次请求的 ID。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ScheduleKeyDeletion
&KeyId=<your-key-id>
&PendingWindowInDays=[7~30]
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
"RequestId": "52ac67cb-3d3d-4ada-b4e2-7047660d3ce9"
}

```

 `XML` 格式

```
//xml response
<KMS>
    <RequestId>52ac67cb-3d3d-4ada-b4e2-7047660d3ce9</RequestId>
</KMS>

```

