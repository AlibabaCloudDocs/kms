# ListAliases

Queries all aliases in the current region for the current account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=ListAliases&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListAliases|The operation that you want to perform. Set the value to ListAliases. |
|PageNumber|Integer|No|1|The number of the page to return.

 Pages start from page 1.

 Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page.

 Valid values: 0 to 100.

 Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Aliases|Array of Alias| |The alias of the user. |
|Alias| | | |
|AliasArn|String|acs:kms:cn-hangzhou:123456:alias/ExampleAlias1|The Alibaba Cloud Resource Name \(ARN\) of the alias. |
|AliasName|String|alias/ExampleAlias1|The ID of the alias. |
|KeyId|String|08c33a6f-4e0a-4a1b-a3fa-7ddfa1d\*\*\*\*|The CMK to which the alias belongs. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|1b57992c-834b-4811-a889-f8bac1ba0353|The ID of the request. |
|TotalCount|Integer|1|The total number of returned aliases. |

## Examples

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ListAliases
&PageNumber=1
&PageSize=10
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
          <Aliases>
                    <Alias>
                              <AliasName>alias/ExampleAlias1</AliasName>
                              <KeyId>08c33a6f-4e0a-4a1b-a3fa-7ddfa1****</KeyId>
                              <AliasArn>acs:kms:cn-hangzhou:123456:alias/ExampleAlias1</AliasArn>
                    </Alias>
          </Aliases>
          <TotalCount>1</TotalCount>
          <PageNumber>1</PageNumber>
          <PageSize>10</PageSize>
          <RequestId>1b57992c-834b-4811-a889-f8bac1ba0353</RequestId>
</KMS>
```

`JSON` format

```
{
        "Aliases": {
                "Alias": [
                        {
                                "AliasName": "alias/ExampleAlias1",
                                "KeyId": "08c33a6f-4e0a-4a1b-a3fa-7ddfa1d****",
                                "AliasArn": "acs:kms:cn-hangzhou:123456:alias/ExampleAlias1"
                        }
        ]
        },
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "1b57992c-834b-4811-a889-f8bac1ba0353"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

