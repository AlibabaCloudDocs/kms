# GetParametersForImport {#concept_68621_zh .concept}

获取导入主密钥（CMK）材料的参数，返回的参数可用于执行[ImportKeyMaterial](cn.zh-CN/API 参考/API列表/ImportKeyMaterial.md#)。

**说明：** 

-   主密钥材料来源是必须外部，即`Origin`为`EXTERNAL`。
-   API 会返回用于加密密钥材料的公钥 \(public key\) ，导入密钥材料的令牌（token），以及令牌的过期时间。公钥是 base64 编码，令牌的有效期为 24 小时。
-   需要指定用于加密密钥材料的公钥类型（目前只支持RSA\_2048），以及加密算法\(目前支持RSAES\_PKCS1\_V1\_5、RSAES\_OAEP\_SHA\_1、RSAES\_OAEP\_SHA\_256三种加密算法\)。
-   本次调用返回的公钥和令牌，只能用于本次调用中指定的 CMK。
-   同次调用返回的公钥和令牌必须搭配使用。
-   加密密钥材料时所使用的算法必须是调用 API 时指定的加密算法。
-   每次调用返回的公钥与令牌都不相同。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|CMK 全局唯一标识符。密钥材料来源必须是外部（`Origin`为`EXTERNAL`）。|
|WrappingAlgorithm|String|是|用于加密密钥材料的算法。|
|WrappingKeySpec|String|是|用于加密密钥材料的公钥类型。|

## 返回参数 { .section}

|名称|类型|描述|
|KeyId|String|CMK 全局唯一标识符，后续调用 [ImportKeyMaterial](cn.zh-CN/API 参考/API列表/ImportKeyMaterial.md#) 时需要指定该参数。|
|ImportToken|String|后续调用 [ImportKeyMaterial](cn.zh-CN/API 参考/API列表/ImportKeyMaterial.md#) 的导入令牌。|
|PublicKey|String|密钥材料导入前，使用该公钥将其加密。|
|TokenExpireTime|String|导入令牌的过期时间。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=GetParametersForImport
&KeyId=<external key id>
&WrappingAlgorithm=<key material encryption algorithm>
&WrappingKeySpec=RSA_2048
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
        "ImportToken":"ImportToken",
        "PublicKey":"PublicKey",
        "KeyId":"KeyId",
        "TokenExpireTime":"2018-01-25T00:01:02Z",
        "RequestId":"8cdf51fd-bcd6-d79a-0ef4-e52c9b5466dc"
}

```

 `XML` 格式

```
//xml response
<KMS>
  <ImportToken>ImportToken</ImportToken>
  <PublicKey>PublicKey</PublicKey>
  <KeyId>KeyId</KeyId>
  <TokenExpireTime>2018-01-25T00:01:02Z</TokenExpireTime>
  <RequestId>8cdf51fd-bcd6-d79a-0ef4-e52c9b5466dc</RequestId>
</KMS>

```

