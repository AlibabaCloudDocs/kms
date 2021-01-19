# GetParametersForImport

调用GetParametersForImport接口获取导入主密钥（CMK）材料的参数。

返回的参数可用于执行[ImportKeyMaterial](~~68621~~)。

**说明：**

-   主密钥材料来源是必须外部，即**Origin**为**EXTERNAL**。
-   需要指定用于加密密钥材料的公钥类型，以及加密算法，见下表。
-   API 会返回用于加密密钥材料的公钥（PublicKey），导入密钥材料的令牌（ImportToken），以及令牌的过期时间。公钥是base64编码，令牌的有效期为24小时。
-   本次调用返回的公钥和令牌，只能用于本次调用中指定的CMK。
-   同次调用返回的公钥和令牌必须搭配使用。
-   加密密钥材料时所使用的算法必须是调用API时指定的加密算法。
-   每次调用返回的公钥与令牌都不相同。

|公钥类型

|加密算法

|说明 |
|------|------|----|
|RSA\_2048

|RSAES\_PKCS1\_V1\_5

 RSAES\_OAEP\_SHA\_1

 RSAES\_OAEP\_SHA\_256

|支持所有地域、任意保护级别的密钥。 |
|EC\_SM2

|SM2PKE

|仅支持导入保护级别为**HSM**的密钥，且密码机检测类型为**国密局商用密码检测认证**的地域（详情请参见[托管密码机简介](~~125803~~)）。 |

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=GetParametersForImport&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetParametersForImport|要执行的操作，取值：**GetParametersForImport**。 |
|KeyId|String|是|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|主密钥全局唯一标识符。

 **说明：** 密钥材料来源必须是外部（**Origin**为**EXTERNAL**）。 |
|WrappingAlgorithm|String|是|RSAES\_PKCS1\_V1\_5|用于加密密钥材料的算法。 |
|WrappingKeySpec|String|是|RSA\_2048|用于加密密钥材料的公钥类型。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ImportToken|String|Base64String|导入令牌。

 后续调用[ImportKeyMaterial](~~68622~~)时需要指定该参数。 |
|KeyId|String|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|主密钥全局唯一标识符。

 后续调用[ImportKeyMaterial](~~68622~~)时需要指定该参数。 |
|PublicKey|String|MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAlls4uIBxD0GG84C+lGBO6Dhpf1J3XimC6cPmPNaKKJMOzoX4tD+C+r7aZv8lZ3vnPfxuxvy/YwG+whUxTEEFUdqJTOIzhPfYucupqKM92crVHIuG+xtMVeHKjyTr+UrtKCsQikqHT+19yDRN/RMoo2HUx0gmEnRyXd8t3JyUXun9FdoxKA08GrsV7nodb9ZsoBLhnev7tTLcXvLyKW6XG1ZQCQm6dPnbnwLeDXR7uK0Lqn9PM28mBIdaiQUQxj2XbM1CoJA+JiyVX3Ptdb+4rqukb4Rb05B80Bs9xV/cf7FIku08l7xGhrGiQFq+DFXwQWtwihXHZxz3LhldU+4ZPwIDAQAB|用于加密密钥材料的公钥。 |
|RequestId|String|8cdf51fd-bcd6-d79a-0ef4-e52c9b5466dc|请求ID。 |
|TokenExpireTime|String|2018-01-25T00:01:02Z|导入令牌的过期时间。 |

## 示例

请求示例

```
https://[Endpoint]/?Action=GetParametersForImport
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&WrappingAlgorithm=RSAES_PKCS1_V1_5
&WrappingKeySpec=RSA_2048
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
    <ImportToken>Base64String</ImportToken>
    <PublicKey>MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAlls4uIBxD0GG84C+lGBO6Dhpf1J3XimC6cPmPNaKKJMOzoX4tD+C+r7aZv8lZ3vnPfxuxvy/YwG+whUxTEEFUdqJTOIzhPfYucupqKM92crVHIuG+xtMVeHKjyTr+UrtKCsQikqHT+19yDRN/RMoo2HUx0gmEnRyXd8t3JyUXun9FdoxKA08GrsV7nodb9ZsoBLhnev7tTLcXvLyKW6XG1ZQCQm6dPnbnwLeDXR7uK0Lqn9PM28mBIdaiQUQxj2XbM1CoJA+JiyVX3Ptdb+4rqukb4Rb05B80Bs9xV/cf7FIku08l7xGhrGiQFq+DFXwQWtwihXHZxz3LhldU+4ZPwIDAQAB</PublicKey>
    <KeyId>KeyId</KeyId>
    <TokenExpireTime>2018-01-25T00:01:02Z</TokenExpireTime>
    <RequestId>8cdf51fd-bcd6-d79a-0ef4-e52c9b5466dc</RequestId>
</KMS>
```

`JSON` 格式

```
{
        "ImportToken":"Base64String",
        "PublicKey":"MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAlls4uIBxD0GG84C+lGBO6Dhpf1J3XimC6cPmPNaKKJMOzoX4tD+C+r7aZv8lZ3vnPfxuxvy/YwG+whUxTEEFUdqJTOIzhPfYucupqKM92crVHIuG+xtMVeHKjyTr+UrtKCsQikqHT+19yDRN/RMoo2HUx0gmEnRyXd8t3JyUXun9FdoxKA08GrsV7nodb9ZsoBLhnev7tTLcXvLyKW6XG1ZQCQm6dPnbnwLeDXR7uK0Lqn9PM28mBIdaiQUQxj2XbM1CoJA+JiyVX3Ptdb+4rqukb4Rb05B80Bs9xV/cf7FIku08l7xGhrGiQFq+DFXwQWtwihXHZxz3LhldU+4ZPwIDAQAB",
        "KeyId":"KeyId",
        "TokenExpireTime":"2018-01-25T00:01:02Z",
        "RequestId":"8cdf51fd-bcd6-d79a-0ef4-e52c9b5466dc"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

