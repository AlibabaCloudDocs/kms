# ListKeys {#concept_28951_zh .concept}

返回调用者在调用区域的所有的主密钥 ID。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|PageNumber|Integer|否|当前页数。有效值：大于 0， 默认值为 1。|
|PageSize|Integer|否|每页返回值的个数。有效值：大于 0，小于 101，默认为 10。|

## 返回参数 { .section}

|名称|类型|描述|
|KeyId|String|主密钥的全局唯一标识符。|
|TotalCount|Integer|主密钥的总数。|
|PageNumber|Integer|当前页数。|
|PageSize|Integer|每页返回值的个数。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ListKeys
&PageNumber=1
&PageSize=10
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
        "Keys": {
                "Key": [
                        {
                                "KeyId": "08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****"
                        },
                        {
                                "KeyId": "0e478b7a-4262-4802-b8cb-00d3fb40****"
                        },
                        {
                                "KeyId": "1abf9b4e-d3dd-4d4b-b9b2-2829043a****"
                        }
                ]
        },
        "TotalCount": 3,
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "1fbcd12a-1b7f-468f-84a3-1ff3444dfd8b"
}

```

 `XML` 格式

```
//xml response
<KMS>
        <Keys>
                <Key>
                        <KeyId>08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****</KeyId>
                </Key>
                <Key>
                        <KeyId>0e478b7a-4262-4802-b8cb-00d3fb40****</KeyId>
                </Key>
                <Key>
                        <KeyId>1abf9b4e-d3dd-4d4b-b9b2-2829043a****</KeyId>
                </Key>
        </Keys>
        <TotalCount>3</TotalCount>
        <PageNumber>1</PageNumber>
        <PageSize>10</PageSize>
        <RequestId>1050b8f1-b264-496d-a782-6299cbaf15f8</RequestId>
</KMS>


```

