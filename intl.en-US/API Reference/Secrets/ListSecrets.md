# ListSecrets

Queries all secrets created by your Alibaba Cloud account in the current region.

This operation returns the metadata information stored in secret objects and does not return encrypted secret values.

In this example, the secrets created by the current account in the current region are returned. The `PageNumber` parameter is set to `1`, and the `PageSize` parameter is set to `2`, which indicates that two secrets are to be returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=ListSecrets&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListSecrets|The operation that you want to perform. Set the value to ListSecrets. |
|FetchTags|String|No|false|Specifies whether to return the resource tags of the secret. Valid values:

 -   true: The resource tags are returned.
-   false: The resource tags are not returned. This is the default value. |
|PageNumber|Integer|No|1|The number of the page to return.

 Pages start from page 1.

 Default value: 1. |
|PageSize|Integer|No|2|The number of entries to return on each page.

 Valid values: 1 to 100

 Default value: 10. |
|Filters|String|No|\[\{"Key":"SecretName", "Values":\["$Val1","$Val2"\]\}\]|The secret filter. Filters are key-values pairs. You can specify one key-values pair or leave this parameter empty. If you filter resources based on tag keys or values, up to 4,000 resources can be returned in the response. To query more than 4,000 resources, call the [ListTagResources](~~120090~~) operation.

 -   Key
    -   Description: the property that you want to filter.
    -   Type: string.
    -   Valid values:
        -   SecretName: the secret name.
        -   Description: the description of the secret.
        -   TagKey: the tag key.
        -   TagValue: the tag value.
-   Values
    -   Description: the value to be included after filtering.
    -   Type: string.
    -   Length: 0 to 10.
    -   Valid values:
        -   If the Key field is set to SecretName, the value must be 1 to 192 characters in length and can contain letters, digits, and special characters. The special characters include `underscores (_), forward slashes (/), plus signs (+), equal signs (=), periods (.), at signs (@), and hyphens (-)`.
        -   If the Key field is set to Description, the value must be 1 to 256 characters in length.
        -   If the Key field is set to TagKey, the value must be 1 to 256 characters in length and can contain letters, digits, and special characters. The special characters include `forward slashes (/), underscores (_), hyphens (-), periods (.), plus signs (+), equal signs (=), at signs (@), and colons (:)`.
        -   If the Key field is set to TagValue, the value must be 1 to 256 characters in length and can contain letters, numbers, and special characters. The special characters include `forward slashes (/), underscores (_), hyphens (-), periods (.), plus signs (+), equal signs (=), at signs (@), and colons (:)`.

 The logical relationship between values for a key in the Filters parameter is OR. Example: `[ {"Key":"SecretName", "Values":["sec1","sec2"]} ]`. In this example, the semantics are `SecretName=sec 1 OR SecretName=sec 2` |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|2|The number of entries returned per page. |
|RequestId|String|6a6287a0-ff34-4780-a790-fdfca900557f|The ID of the request. |
|SecretList|Array of Secret| |The list of secrets. |
|Secret| | | |
|CreateTime|String|2020-07-17T07:59:05Z|The time when the secret was created. |
|PlannedDeleteTime|String|2020-08-17T07:59:05Z|The time when the secret is scheduled to be deleted. |
|SecretName|String|secret001|The name of the secret. |
|SecretType|String|Generic|The type of the secret. Valid values:

 -   Generic: indicates a standard secret.
-   Rds: indicates a managed ApsaraDB RDS secret. |
|Tags|Array of Tag| |The resource tags of the secret.

 If the FetchTags parameter is set to false or is not specified, this parameter is not returned. |
|Tag| | | |
|TagKey|String|key1|The tag key. |
|TagValue|String|val1|The tag value. |
|UpdateTime|String|2020-07-17T07:59:05Z|The time when the secret was updated. |
|TotalCount|Integer|55|The number of returned secrets. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ListSecrets
&PageNumber=1
&PageSize=2
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <SecretList>
		    <Secret>
			      <SecretName>secret001</SecretName>
			      <SecretType>Generic</SecretType>
			      <CreateTime>2020-07-17T07:59:05Z</CreateTime>
			      <UpdateTime>2020-07-17T07:59:05Z</UpdateTime>
		    </Secret>
		    <Secret>
			      <SecretName>cache_client</SecretName>
			      <SecretType>Generic</SecretType>
			      <CreateTime>2020-07-23T11:56:29Z</CreateTime>
			      <UpdateTime>2021-01-12T02:15:42Z</UpdateTime>
		    </Secret>
	  </SecretList>
	  <RequestId>6a6287a0-ff34-4780-a790-fdfca900557f</RequestId>
	  <PageNumber>1</PageNumber>
	  <PageSize>2</PageSize>
	  <TotalCount>55</TotalCount>
</KMS>
```

`JSON` format

```
{
	"SecretList": {
		"Secret": [
			{
				"SecretName": "secret001",
				"SecretType": "Generic",
				"CreateTime": "2020-07-17T07:59:05Z",
				"UpdateTime": "2020-07-17T07:59:05Z"
			},
			{
				"SecretName": "cache_client",
				"SecretType": "Generic",
				"CreateTime": "2020-07-23T11:56:29Z",
				"UpdateTime": "2021-01-12T02:15:42Z"
			}
		]
	},
	"RequestId": "6a6287a0-ff34-4780-a790-fdfca900557f",
	"PageNumber": 1,
	"PageSize": 2,
	"TotalCount": 55
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

