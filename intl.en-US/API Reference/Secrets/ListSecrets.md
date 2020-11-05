# ListSecrets

Queries all secrets created by your Alibaba Cloud account in the current region.

This operation returns the metadata information stored in secret objects and does not return encrypted secret values.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=ListSecrets&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListSecrets|The operation that you want to perform. Set the value to ListSecrets. |
|FetchTags|String|No|false|Specifies whether to return the resource tags of the secrets. Valid values:

-   true: The resource tags are returned.
-   false: The resource tags are not returned. This is the default value. |
|PageNumber|Integer|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page.

Valid values: 1 to 100.

Default value: 10. |
|Filters|String|No|\[\{"Key":"SecretName", "Values":\["$Val1","$Val2"\]\}\]|The secret filter. The filter consists of one key-values pair.

-   Key
    -   Description: the property that you want to filter.
    -   Type: string.
    -   Valid values:
        -   SecretName: the secret name.
        -   Description: the description of the secret.
        -   TagKey: the tag key
        -   TagValue: the tag value
-   Values
    -   Description: the value to be included after filtering.
    -   Type: string.
    -   Length: 0 to 10.
    -   Valid values:
        -   When Key is set to SecretName, the value must be 1 to 192 characters in length and can contain letters, digits, and special characters`_ / + = @ -`.
        -   When Key is set to Description, the value must be 1 to 256 characters in length.
        -   When Key is set to TagKey, the value must be 1 to 256 characters in length and can contain letters, digits, and special characters`/ _ - + =@:`.
        -   When Key is set to TagValue, the value must be 1 to 256 characters in length and can contain letters, numbers, and special characters`/ _ - + =@:`.

The logical relationship between values for a key is OR. Example: `[ {"Key":"SecretName", "Values":["sec1","sec2"]}]`. In this example, the semantics are:`(secretname=sec 1OR secretname=sec 2)` |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|e8818e65-5c5b-4a0e-a571-8f50b59920a7|The ID of the request. |
|SecretList|Array of Secret| |The list of secrets. |
|Secret| | | |
|CreateTime|String|2020-02-21T01:24:45Z|The time when a secret was created. |
|PlannedDeleteTime|String|2020-03-21T01:24:45Z|The time when a secret is scheduled to be deleted. |
|SecretName|String|secret001|The name of a secret. |
|Tags|Array of Tag| |The resource tags of secrets. If the request parameter FetchTags is set to false, this parameter is not returned. |
|Tag| | | |
|TagKey|String|key1|The key of a resource tag. |
|TagValue|String|val1|The value of a resource tag. |
|UpdateTime|String|2020-02-21T15:22:45Z|The time when a secret was updated. |
|TotalCount|Integer|20|The number of returned secrets. |

## Examples

Sample requests

```
ttps://kms.cn-hangzhou.aliyuncs.com/? Action=ListSecrets
&PageNumber=1
&PageSize=10
&Filters=[{"Key":"SecretName", "Values":["$Val1","$Val2"]}]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SecretList>
    <Secret>
        <SecretName>secret001</SecretName>
        <CreateTime>2020-02-21T01:24:45Z</CreateTime>
        <UpdateTime>2020-02-21T01:24:45Z</UpdateTime>
        <Tags>
        </Tags>
    </Secret>
    <Secret>
        <SecretName>secret004</SecretName>
        <CreateTime>2020-02-21T15:22:45Z</CreateTime>
        <UpdateTime>2020-02-21T15:22:45Z</UpdateTime>
        <Tags>
            <Tag>
                <TagKey>key1</TagKey>
                <TagValue>val1</TagValue>
            </Tag>
            <Tag>
                <TagKey>key2</TagKey>
                <TagValue>val2</TagValue>
            </Tag>
        </Tags>
    </Secret>
</SecretList>
<RequestId>edbdc10d-3bcb-4690-95cb-3bf5664e1f02</RequestId>
<PageNumber>1</PageNumber>
<PageSize>10</PageSize>
<TotalCount>2</TotalCount>
```

`JSON` format

```
{
    "SecretList": {
        "Secret": [
            {
                "SecretName": "secret001",
                "CreateTime": "2020-02-21T01:24:45Z",
                "UpdateTime": "2020-02-21T01:24:45Z",
                "Tags": {
                    "Tag": []
                }
            },
            {
                "SecretName": "secret004",
                "CreateTime": "2020-02-21T15:22:45Z",
                "UpdateTime": "2020-02-21T15:22:45Z",
                "Tags": {
                    "Tag": [
                        {
                            "TagKey": "key1",
                            "TagValue": "val1"
                        },
                        {
                            "TagKey": "key2",
                            "TagValue": "val2"
                        }
                    ]
                }
            }
        ]
    },
    "RequestId": "edbdc10d-3bcb-4690-95cb-3bf5664e1f02",
    "PageNumber": 1,
    "PageSize": 10,
    "TotalCount": 2
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

