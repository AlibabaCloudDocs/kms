# ScheduleKeyDeletion

调用ScheduleKeyDeletion接口申请删除一个指定的主密钥（CMK\)。

在密钥预删除期间，密钥状态处于待删除状态，无法用于加密、解密、产生数据密钥操作。

主密钥一旦删除，将无法恢复，使用该主密钥加密的内容及产生的数据密钥也将无法解密。因此，对于主密钥的删除，KMS只提供申请删除的方式，而不提供直接删除的方式。如果您有删除密钥方面的需求，可以通过[DisableKey](~~35151~~)禁用密钥。

在申请删除主密钥的同时，需要指定一个预删除周期，该周期最少为7天，最多为30天。从申请删除主密钥的时刻开始，到删除周期之前，可以通过[CancelKeyDeletion](~~44197~~)撤销密钥删除的申请。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=ScheduleKeyDeletion&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ScheduleKeyDeletion|要执行的操作，取值：ScheduleKeyDeletion。 |
|KeyId|String|是|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|密钥ID。CMK全局唯一标识符。 |
|PendingWindowInDays|Integer|否|7|密钥预删除周期。在这段时间内，您可以撤销删除处于待删除状态的密钥；预删除时间过后无法撤销删除。

 取值范围：7~30。

 单位：天。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|3da5b8cc-8107-40ac-a170-793cd181d7b7|请求ID。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ScheduleKeyDeletion
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
      <RequestId>3da5b8cc-8107-40ac-a170-793cd181d7b7</RequestId>
</KMS>
```

`JSON` 格式

```
{
"RequestId": "3da5b8cc-8107-40ac-a170-793cd181d7b7"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Throttling|Request was denied due to request throttling.|您这个时段的流量已经超限。如果不能满足现有业务要求可以提工单进行申请。|
|404|Forbidden.KeyNotFound|The specified Key is not found.|指定的密钥不存在。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

