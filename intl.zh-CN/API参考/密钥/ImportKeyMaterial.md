# ImportKeyMaterial

调用ImportKeyMaterial接口导入密钥材料。

调用[CreateKey](~~28947~~)创建主密钥时，可以选择其密钥材料来源为外部，即将**Origin**设置为**EXTERNAL**。此API用于将密钥材料导入符合上述描述的CMK中。

-   要查看CMK的**Origin**，请参见[DescribeKey](~~28952~~)。
-   在导入密钥材料之前， 需要调用[GetParametersForImport](~~68621~~)先获得导入密钥材料需要的参数，即用于加密密钥材料的公钥（PublicKey）和导入令牌（ImportToken）。

**说明：**

-   对密钥类型为**Aliyun\_AES\_256**的CMK，密钥材料必须为256位；对密钥类型为**Aliyun\_SM4**的CMK，密钥材料必须为128位。
-   您可以为密钥材料设置过期时间，也可以设置其永不过期。
-   您可以随时为指定的CMK重新导入密钥材料，并重新指定过期时间，但必须导入相同的密钥材料。
-   导入的密钥材料过期或者被删除后，指定的CMK将无法使用，需要再次导入相同的密钥材料才可正常使用。
-   同样的密钥材料可导入不同的CMK中，但使用其中一个CMK加密的数据或生成的数据密钥（Data Key）无法使用另一个CMK解密。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=ImportKeyMaterial&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ImportKeyMaterial|要执行的操作，取值：**ImportKeyMaterial**。 |
|EncryptedKeyMaterial|String|是|bCPZx7I6v6KXsqEpr2OXKxuj2CCRtKdwp75Bw+BGncYqBdfjFBYRtOE6HRlT0oeiRDWzwnw9OA54OL36smDJrq4Lo9x0CyYDiuKnRkcKtMtlzW0din7Pd7IlZWWRdVueiw2qpzl7PkUWQGTdsdbzpfJJQ+qj/cRIrk/E83UGyeyytSpgnb+lu0xEYcPajRyWNsbi98N3pqqQzHXNNHO2NJqHlnQgglqTiBEjkGeKFhfKmTc3vjulIdVa3EaVIN6lwWfgx+UUYSrvbA77WDYKlDsZ4SbK2/T7za9Tp1qU7Ynqba7OKGVVj7PMbiaO80AxWZnjUMYCgEp5w7V+seOXqw==|使用**GetParametersForImport**返回的公钥加密并用base64编码后的密钥材料。 |
|ImportToken|String|是|Base64String|通过调用**GetParametersForImport**获得的导入令牌。 |
|KeyId|String|是|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|待导入的主密钥ID。 |
|KeyMaterialExpireUnix|Long|是|0|密钥材料过期时间。

 不指定该参数或取值为0，表示密钥材料不会过期。

 **说明：** 取值不可早于调用该API的时间（以服务器时间为准）。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|ec1017cf-ead4-f3ca-babc-c3b34f3dbecb|请求ID。 |

## 示例

请求示例

```
https://[Endpoint]/?Action=ImportKeyMaterial
&EncryptedKeyMaterial=bCPZx7I6v6KXsqEpr2OXKxuj2CCRtKdwp75Bw+BGncYqBdfjFBYRtOE6HRlT0oeiRDWzwnw9OA54OL36smDJrq4Lo9x0CyYDiuKnRkcKtMtlzW0din7Pd7IlZWWRdVueiw2qpzl7PkUWQGTdsdbzpfJJQ+qj/cRIrk/E83UGyeyytSpgnb+lu0xEYcPajRyWNsbi98N3pqqQzHXNNHO2NJqHlnQgglqTiBEjkGeKFhfKmTc3vjulIdVa3EaVIN6lwWfgx+UUYSrvbA77WDYKlDsZ4SbK2/T7za9Tp1qU7Ynqba7OKGVVj7PMbiaO80AxWZnjUMYCgEp5w7V+seOXqw==
&ImportToken=Base64String
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&KeyMaterialExpireUnix=0
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
    <RequestId>ec1017cf-ead4-f3ca-babc-c3b34f3dbecb</RequestId>
</KMS>
```

`JSON` 格式

```
{
        "RequestId":"ec1017cf-ead4-f3ca-babc-c3b34f3dbecb"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

