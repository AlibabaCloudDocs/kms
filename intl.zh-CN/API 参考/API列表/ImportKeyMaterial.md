# ImportKeyMaterial {#concept_68622_zh .concept}

调用[CreateKey](cn.zh-CN/API 参考/API列表/CreateKey.md#)创建主密钥时，可以选择其密钥材料来源为外部，即将`Origin`设置为`EXTERNAL`，并在创建时不导入密钥材料。此 API 用于将密钥材料导入符合上述描述的 CMK 中。

-   要查看 CMK 的`Origin`，请参见[3DescribeKey](cn.zh-CN/API 参考/API列表/DescribeKey.md#)。

-   在导入密钥材料之前， 需要调用[GetParametersForImport](cn.zh-CN/API 参考/API列表/GetParametersForImport.md#)先获得导入密钥材料需要的参数，即用于加密密钥材料的公钥（public key）和导入令牌（token）。


**说明：** 

-   密钥材料只能是 256 位的对称密钥。
-   您可以为密钥材料设置过期时间，也可以设置其永不过期。
-   您可以随时为指定的 CMK 重新导入密钥材料，并重新指定过期时间。但必须导入相同的密钥材料，某个指定的 CMK 不可以更换密钥材料。
-   导入的密钥材料过期或者被删除后，指定的CMK将无法使用，需要再次导入相同的密钥材料才可正常使用。
-   同样的密钥材料可导入不同的 CMK 中，但使用其中一个 CMK 加密的数据或 Datakey，无法使用另一个 CMK解密。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|EncryptedKeyMaterial|String|是|Base64 加密后的密钥材料。|
|ImportToken|String|是|通过调用`GetParametersForImport`获得的导入令牌。|
|KeyMaterialExpireUnix|Timestamp|否|密钥材料过期时间。- 不指定该参数，或取值为 0 表示密钥材料不会过期。- 取值不可早于调用该API 的时间（以服务器时间为准）。|

## 返回参数 { .section}

|名称|类型|描述|
|RequestId|String|本次请求的 ID。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ImportKeyMaterial
&EncryptedKeyMaterial=<your encrypted key material>
&ImportToken=<import token from GetParametersForImport>
&KeyMaterialExpireUnix=1518307200
&<公共请求参数>

```

**返回示例**

 `JSON`格式

```
//json response
{
        "RequestId":"ec1017cf-ead4-f3ca-babc-c3b34f3dbecb"
}

```

 `XML`格式

```
//xml response
<KMS>
  <RequestId>ec1017cf-ead4-f3ca-babc-c3b34f3dbecb</RequestId>
</KMS>

```

