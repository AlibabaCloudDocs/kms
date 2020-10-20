# ListKeys

调用ListKeys查询调用者在调用地域的所有主密钥ID。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=ListKeys&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListKeys|要执行的操作，取值：ListKeys。 |
|PageNumber|Integer|否|1|当前页数。

 取值范围：大于0。

 默认值：1。 |
|PageSize|Integer|否|10|每页返回值的个数。

 取值范围：1~100。

 默认值：10。 |
|Filters|String|否|\[\{"Key":"KeyState", "Values":\["Enabled","Disabled"\]\}\]|主密钥过滤器。由Key-Values键值对组成，长度为0~10。

 -   Key
    -   描述：需要过滤的属性。
    -   类型：String。
    -   取值：
        -   KeyState：密钥状态。
        -   KeySpec：密钥类型。
        -   KeyUsage：密钥用途。
        -   ProtectionLevel：保护等级。
        -   CreatorType：创建者类型。
-   Values
    -   描述：期望过滤后包含的值。
    -   类型：String数组。
    -   长度：0~10。
    -   取值：
        -   Key取值为KeyState时：Enabled（启用）、Disabled（禁用）、PendingDeletion（待删除）、PendingImport（待导入）。
        -   Key取值为KeySpec时：Aliyun\_AES\_256、Aliyun\_SM4、RSA\_2048、EC\_P256、EC\_P256K、EC\_SM2。

说明：仅在支持托管密码机且已通过国密局商用密码检测认证的地域可以创建EC\_SM2和Aliyun\_SM4类型的密钥，地域详情请参见[支持的地域](~~125803~~)。如果您所选择地域不支持EC\_SM2和Aliyun\_SM4，指定这两个参数将被忽略。

        -   Key取值为KeyUsage时：ENCRYPT/DECRYPT（数据加密和解密）、SIGN/VERIFY （产生和验证数字签名）。
        -   Key取值为ProtectionLevel时：SOFTWARE（软件）、HSM（硬件）。

说明：HSM保护等级仅在特定地域支持，地域详情请参见[支持的地域](~~125803~~)。如您所选择地域不支持HSM，指定该参数将被忽略。

        -   Key取值为CreatorType时：User（获取由用户创建的主密钥）、Service （获取由用户授权其他云产品自动创建的主密钥）。

 Filters不同Key之间的逻辑关系为AND，同一个Key中的多个Value之间的逻辑关系为OR。例如：输入

 `[ {"Key":"KeyState", "Values":["Enabled","Disabled"]}, {"Key":"KeyState", "Values":["PendingDeletion"]}, {"Key":"KeySpec", "Values":["Aliyun_AES_256"]} ]`时，语义为：`(KeyState=Enabled OR KeyState=Disabled OR KeyState=PendingDeletion) AND (KeySpec=Aliyun_AES_256)`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Keys|Array of Key| |主密钥。 |
|Key| | | |
|KeyArn|String|acs:kms:cn-hangzhou:123456:key/80e9409f-78fa-42ab-84bd-83f40c81\*\*\*\*|主密钥的ARN。 |
|KeyId|String|08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4\*\*\*\*|主密钥的全局唯一标识符。 |
|PageNumber|Integer|1|当前页数。 |
|PageSize|Integer|10|每页返回值的个数。 |
|RequestId|String|1050b8f1-b264-496d-a782-6299cbaf15f8|请求ID。 |
|TotalCount|Integer|3|主密钥的总数。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ListKeys
&PageNumber=1
&PageSize=10
&Filters=[{"Key":"KeyState", "Values":["Enabled","Disabled"]}]
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
          <Keys>
                    <Key>
                              <KeyId>80e9409f-78fa-42ab-84bd-83f40c81****</KeyId>
                              <KeyArn>acs:kms:cn-hangzhou:123456:key/80e9409f-78fa-42ab-84bd-83f40c81****</KeyArn>
                    </Key>
                    <Key>
                              <KeyId>8fbb1226-a06f-4c57-8887-daa5b627****</KeyId>
                              <KeyArn>acs:kms:cn-hangzhou:123456:key/8fbb1226-a06f-4c57-8887-daa5b627****</KeyArn>
                    </Key>
                      </Keys>
          <TotalCount>3</TotalCount>
          <PageNumber>1</PageNumber>
          <PageSize>10</PageSize>
          <RequestId>bc29ec35-3373-48d1-8202-520fd78d****</RequestId>
</KMS>
```

`JSON` 格式

```
{
        "Keys": {
                "Key": [
                        {
                                "KeyId": "80e9409f-78fa-42ab-84bd-83f40c81****",
				                "KeyArn": "acs:kms:cn-hangzhou:123456:key/80e9409f-78fa-42ab-84bd-83f40c81****"                        
                        },
                        {
                                "KeyId": "8fbb1226-a06f-4c57-8887-daa5b627****",
				                "KeyArn": "acs:kms:cn-hangzhou:123456:key/8fbb1226-a06f-4c57-8887-daa5b627****"
                        }
                    ],
                "TotalCount": 3,
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "bc29ec35-3373-48d1-8202-520fd78d****"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

