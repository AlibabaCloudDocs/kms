# ListKeys {#concept_28951_zh .concept}

Returns a list of all CMKs in the caller’s account and region.

## Request parameters { .section}

|Name|Type|Required|Description|
|PageNumber|Integer|No|The current page number. It must be an integer greater than 0. The default value is 1.|
|PageSize|Integer|No|The number of items on each page. It must be an integer greater than 0 and no more than 101. The default value is 10.|

## Response parameters { .section}

|Name|Type|Description|
|KeyId|String|Globally unique identifier of the key.|
|TotalCount|Integer|The total number of keys.|
|PageNumber|Integer|The current page number.|
|PageSize|Integer|The number of items on each page.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ListKeys
&PageNumber=1
&PageSize=10
&<Common Request Parameters>

```

**Response example**

 `JSON` format

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

 `XML` format

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

