# CreateKey

调用CreateKey接口创建一个主密钥。

主密钥可以是对称密钥或非对称密钥。对称密钥主要用于生成可以加密大量数据的DataKey，有时也直接用于加密少量数据（少于6KB）。更多信息，请参见[GenerateDataKey](~~28948~~) 。非对称密钥用于加密解密或签名验签，但无法生成数据密钥。

各种密钥类型支持的操作如下表所示：

|密钥类型

|KeySpec

|说明

|加密解密

|签名验签 |
|------|---------|----|------|------|
|对称密钥

|Aliyun\_AES\_256

|AES密钥，长度为256比特

|支持

|不支持 |
|对称密钥

|Aliyun\_SM4

|SM4密钥

|支持

|不支持 |
|非对称密钥

|RSA\_2048

|RSA密钥，模长为2048比特

|支持

|支持 |
|非对称密钥

|RSA\_3072

|RSA密钥，模长为3072比特

|支持

|支持 |
|非对称密钥

|EC\_P256

|NIST推荐椭圆曲线P-256（secp256r1）

|不支持

|支持 |
|非对称密钥

|EC\_P256K

|SECG椭圆曲线secp256k1

|不支持

|支持 |
|非对称密钥

|EC\_SM2

|GBT32918定义的素数域256位椭圆曲线

|支持

|支持 |

**说明：**

-   对称密钥KeySpec在标准密钥类型前加上`Aliyun_`前缀，表示使用标准密钥的密码算法，但是会生成非标准密文；非对称密钥产生标准密文或者签名。
-   RSA密钥使用方式仅支持ENCRYPT/DECRYPT、SIGN/VERIFY两者之一，单个密钥无法同时支持两种操作。
-   SM4和SM2为中国国家密码管理局批准的密码算法，KMS通过部署在中国内地的托管密码机提供支持。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=CreateKey&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateKey|要执行的操作，取值：CreateKey。 |
|Description|String|否|key description example|密钥的描述。

 长度为0~8192个字符。 |
|KeySpec|String|否|Aliyun\_AES\_256|密钥的类型，取值：

 -   Aliyun\_AES\_256
-   Aliyun\_SM4
-   RSA\_2048
-   RSA\_3072
-   EC\_P256
-   EC\_P256K
-   EC\_SM2

 **说明：** 在中国内地使用托管密码机创建的密钥，默认为Aliyun\_SM4类型，其余情况下默认为Aliyun\_AES\_256。 |
|KeyUsage|String|否|ENCRYPT/DECRYPT|密钥的用途，取值：

 -   ENCRYPT/DECRYPT：数据加密和解密。
-   SIGN/VERIFY：产生和验证数字签名。 |
|Origin|String|否|Aliyun\_KMS|密钥材料来源，取值：

 -   Aliyun\_KMS（默认值）
-   EXTERNAL

 **说明：**

-   请注意区分大小写。
-   当KeySpec为非对称密钥类型时禁止选择EXTERNAL。
-   如果选择EXTERNAL，您需要[导入密钥材料](~~68523~~)。 |
|ProtectionLevel|String|否|SOFTWARE|密钥的保护级别，取值：

 -   SOFTWARE（默认值）
-   HSM

 **说明：**

-   请注意区分大小写。
-   当取值为HSM时，如果Origin参数为Aliyun\_KMS，则会在托管密码机中生成密钥，用于执行密码运算；如果Origin参数为EXTERNAL，您可以将外部密钥导入到托管密码机中，用于执行密码运算。 |
|EnableAutomaticRotation|Boolean|否|false|是否开启自动密钥轮转，取值：

 -   true
-   false（默认值）

 **说明：** 若Origin为EXTERNAL或KeySpec为非对称密钥类型则无法支持自动轮转。 |
|RotationInterval|String|否|365d|自动轮转的时间周期。格式为integer\[unit\]，其中integer表示时间长度，unit表示时间单位。合法的unit单位为：d（天）、h（小时）、m（分钟）、s（秒）。7d或者604800s均表示7天的周期。取值：7~730天。

 **说明：** 当EnableAutomaticRotation参数为true时，必须设置此参数；否则，将忽略此参数。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|KeyMetadata|Struct| |主密钥（CMK）的metadata。 |
|Arn|String|acs:kms:cn-qingdao:154035569884\*\*\*\*:key/d6bee1cb-2e14-4277-ba6b-73786b21\*\*\*\*|主密钥ARN。 |
|AutomaticRotation|String|Disabled|是否开启自动密钥轮转，取值：

 -   Enabled：自动轮转处于开启状态。
-   Disabled：自动轮转处于未开启状态。
-   Suspended：自动轮转被暂停执行，详情请参见[自动轮转密钥](~~134270~~)。

 **说明：** 仅适用于对称类型的CMK，非对称类型的CMK不支持自动轮转。 |
|CreationDate|String|2016-03-25T10:42:40Z|创建主密钥的日期和时间（UTC）。 |
|Creator|String|154035569884\*\*\*\*|主密钥创建者。 |
|DeleteDate|String|2020-07-06T18:22:03Z|主密钥的预计删除时间。

 更多信息，请参见[ScheduleKeyDeletion](~~44196~~)。

 **说明：** 只有当KeyState值为PendingDeletion时，返回该值。 |
|Description|String|key description example|主密钥的描述。 |
|KeyId|String|d6bee1cb-2e14-4277-ba6b-73786b21\*\*\*\*|主密钥的全局唯一标识符。 |
|KeySpec|String|Aliyun\_AES\_256|主密钥的类型。 |
|KeyState|String|Enabled|主密钥的状态。

 详情请参见[用户主密钥的状态对API调用的影响](~~44211~~)。 |
|KeyUsage|String|ENCRYPT/DECRYPT|主密钥的用途。 |
|LastRotationDate|String|2019-06-06T18:22:03Z|最近一次轮转的时间（UTC）。

 如果是新创建密钥，则为初始密钥版本生成时间。 |
|MaterialExpireTime|String|2020-07-06T18:22:03Z|密钥材料的过期时间（UTC）。

 当该值为空时，表示密钥材料不会过期。 |
|NextRotationDate|String|2020-07-06T18:22:03Z|下一次轮转的时间。

 **说明：** 只有当AutomaticRotation参数值为Enabled或Suspended时，返回该值。 |
|Origin|String|Aliyun\_KMS|主密钥的密钥材料来源。 |
|PrimaryKeyVersion|String|7ce1d081-06cb-42e6-aab6-5c5de030\*\*\*\*|对称类型主密钥的当前主版本标志符。

 **说明：**

-   主版本是对称类型主密钥的活跃加密密钥，密钥管理使用主版本处理加密请求。
-   不适用于非对称类型的主密钥。 |
|ProtectionLevel|String|SOFTWARE|密钥的保护级别。 |
|RotationInterval|String|31536000s|密钥自动轮转的周期（秒数）。格式为整数值后加上字符s。例如，7天的轮转周期为604800s。只有当AutomaticRotation参数值为Enabled或Suspended时，返回该值。 |
|RequestId|String|36c7e41a-3f2c-45f7-9bdd-d1dc1e7e7e06|请求ID。 |

## 示例

请求示例

```
https://[Endpoint]/?Action=CreateKey
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <KeyMetadata>
		    <CreationDate>2021-04-12T06:00:54Z</CreationDate>
		    <Description></Description>
		    <KeyId>d6bee1cb-2e14-4277-ba6b-73786b21****</KeyId>
		    <KeySpec>Aliyun_AES_256</KeySpec>
		    <KeyState>Enabled</KeyState>
		    <KeyUsage>ENCRYPT/DECRYPT</KeyUsage>
		    <PrimaryKeyVersion>7ce1d081-06cb-42e6-aab6-5c5de030****</PrimaryKeyVersion>
		    <DeleteDate></DeleteDate>
		    <Creator>154035569884****</Creator>
		    <Arn>acs:kms:cn-qingdao:154035569884****:key/d6bee1cb-2e14-4277-ba6b-73786b21****</Arn>
		    <Origin>Aliyun_KMS</Origin>
		    <MaterialExpireTime></MaterialExpireTime>
		    <ProtectionLevel>SOFTWARE</ProtectionLevel>
		    <LastRotationDate>2021-04-12T06:00:54Z</LastRotationDate>
		    <AutomaticRotation>Disabled</AutomaticRotation>
	  </KeyMetadata>
	  <RequestId>36c7e41a-3f2c-45f7-9bdd-d1dc1e7e7e06</RequestId>
</KMS>
```

`JSON`格式

```
{
  "KeyMetadata": {
    "CreationDate": "2021-04-12T06:00:54Z",
    "Description": "",
    "KeyId": "d6bee1cb-2e14-4277-ba6b-73786b21****",
    "KeySpec": "Aliyun_AES_256",
    "KeyState": "Enabled",
    "KeyUsage": "ENCRYPT/DECRYPT",
    "PrimaryKeyVersion": "7ce1d081-06cb-42e6-aab6-5c5de030****",
    "DeleteDate": "",
    "Creator": "154035569884****",
    "Arn": "acs:kms:cn-qingdao:154035569884****:key/d6bee1cb-2e14-4277-ba6b-73786b21****",
    "Origin": "Aliyun_KMS",
    "MaterialExpireTime": "",
    "ProtectionLevel": "SOFTWARE",
    "LastRotationDate": "2021-04-12T06:00:54Z",
    "AutomaticRotation": "Disabled"
  },
  "RequestId": "36c7e41a-3f2c-45f7-9bdd-d1dc1e7e7e06"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

