# DescribeKey

调用DescribeKey接口查询用户主密钥（CMK）详情。

本文将提供一个示例，为您查询ID为`05754286-3ba2-4fa6-8d41-4323aca6****`的用户主密钥的详情，包括创建者、创建时间、密钥状态、删除保护状态等信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=DescribeKey&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeKey|要执行的操作，取值：DescribeKey。 |
|KeyId|String|是|05754286-3ba2-4fa6-8d41-4323aca6\*\*\*\*|CMK的全局唯一标识符。

 该参数也可以被指定为CMK绑定的别名。更多信息，请参见[别名概述](~~68522~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|KeyMetadata|Struct| |CMK的元数据。 |
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:key/05754286-3ba2-4fa6-8d41-4323aca6\*\*\*\*|CMK ARN。 |
|AutomaticRotation|String|Disabled|是否开启自动轮转，取值：

 -   Enabled：开启自动轮转。
-   Disabled：关闭自动轮转。
-   Suspended：暂停执行自动轮转。

 更多信息，请参见[自动轮转密钥](~~134270~~)。

 **说明：** 仅对称密钥支持自动轮转。 |
|CreationDate|String|2021-05-20T06:34:21Z|CMK的创建时间（UTC）。 |
|Creator|String|154035569884\*\*\*\*|CMK的创建者（阿里云账号）。 |
|DeleteDate|String|2021-05-26T18:22:03Z|CMK的预计删除时间（UTC）。

 更多信息，请参见[ScheduleKeyDeletion](~~44196~~)。

 **说明：** 当KeyState取值为PendingDeletion时，返回该参数。 |
|DeletionProtection|String|Enabled|是否开启删除保护，取值：

 -   Enabled：开启删除保护。
-   Disabled：关闭删除保护。 |
|DeletionProtectionDescription|String|该密钥正在被XXX服务使用。已为您设置删除保护。|删除保护描述。 |
|Description|String|key description example|CMK的描述。 |
|KeyId|String|05754286-3ba2-4fa6-8d41-4323aca6\*\*\*\*|CMK的全局唯一标识符。 |
|KeySpec|String|Aliyun\_AES\_256|CMK的类型。 |
|KeyState|String|Enabled|CMK的状态。

 更多信息，请参见[用户主密钥的状态对API调用的影响](~~44211~~)。 |
|KeyUsage|String|ENCRYPT/DECRYPT|CMK的用途。 |
|LastRotationDate|String|2021-05-20T06:34:21Z|最近一次轮转的时间（UTC）。如果是新创建的密钥，则为初始密钥版本生成时间。 |
|MaterialExpireTime|String|2021-07-06T18:22:03Z|密钥材料的过期时间（UTC）。当该值为空时，表示密钥材料不会过期。 |
|NextRotationDate|String|2021-07-06T18:22:03Z|下一次轮转的时间。

 **说明：** 当AutomaticRotation取值为Enabled或Suspended时，返回该参数。 |
|Origin|String|Aliyun\_KMS|CMK的密钥材料来源。 |
|PrimaryKeyVersion|String|515e0b0a-624f-45ab-92b5-54f9b551\*\*\*\*|对称类型CMK当前的主版本标识符。 |
|ProtectionLevel|String|HSM|密钥的保护级别。 |
|RotationInterval|String|31536000s|密钥自动轮转的周期。

 单位：s。

 例如：7天的轮转周期为604800s。

 **说明：** 当AutomaticRotation取值为Enabled或Suspended时，返回该参数。 |
|RequestId|String|f1fdfa9d-bd49-418b-942f-8f3e3ec00a4f|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribeKey
&KeyId=05754286-3ba2-4fa6-8d41-4323aca6****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <KeyMetadata>
		    <CreationDate>2021-05-20T06:34:21Z</CreationDate>
		    <Description></Description>
		    <KeyId>05754286-3ba2-4fa6-8d41-4323aca6****</KeyId>
		    <KeySpec>Aliyun_AES_256</KeySpec>
		    <KeyState>Enabled</KeyState>
		    <KeyUsage>ENCRYPT/DECRYPT</KeyUsage>
		    <PrimaryKeyVersion>515e0b0a-624f-45ab-92b5-54f9b551****</PrimaryKeyVersion>
		    <DeleteDate></DeleteDate>
		    <Creator>154035569884****</Creator>
		    <Arn>acs:kms:cn-hangzhou:154035569884****:key/05754286-3ba2-4fa6-8d41-4323aca6****</Arn>
		    <Origin>Aliyun_KMS</Origin>
		    <MaterialExpireTime></MaterialExpireTime>
		    <ProtectionLevel>HSM</ProtectionLevel>
		    <LastRotationDate>2021-05-20T06:34:21Z</LastRotationDate>
		    <AutomaticRotation>Disabled</AutomaticRotation>
		    <DeletionProtection>Enabled</DeletionProtection>
	  </KeyMetadata>
	  <RequestId>f1fdfa9d-bd49-418b-942f-8f3e3ec00a4f</RequestId>
</KMS>
```

`JSON`格式

```
{
	"KeyMetadata": {
		"CreationDate": "2021-05-20T06:34:21Z",
		"Description": "",
		"KeyId": "05754286-3ba2-4fa6-8d41-4323aca6****",
		"KeySpec": "Aliyun_AES_256",
		"KeyState": "Enabled",
		"KeyUsage": "ENCRYPT/DECRYPT",
		"PrimaryKeyVersion": "515e0b0a-624f-45ab-92b5-54f9b551****",
		"DeleteDate": "",
		"Creator": "154035569884****",
		"Arn": "acs:kms:cn-hangzhou:154035569884****:key/05754286-3ba2-4fa6-8d41-4323aca6****",
		"Origin": "Aliyun_KMS",
		"MaterialExpireTime": "",
		"ProtectionLevel": "HSM",
		"LastRotationDate": "2021-05-20T06:34:21Z",
		"AutomaticRotation": "Disabled",
		"DeletionProtection": "Enabled"
	},
	"RequestId": "f1fdfa9d-bd49-418b-942f-8f3e3ec00a4f"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|Forbidden.KeyNotFound|The specified Key is not found.|指定的密钥不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

