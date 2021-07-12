# CreateKeyVersion

Creates a version for a customer master key \(CMK\).

Limits:

-   You can create a version only for an asymmetric CMK that is in the Enabled state. You can call the [CreateKey](~~28947~~) operation to create an asymmetric CMK and the [DescribeKey](~~28952~~) operation to query the status of the CMK. The status is specified by the KeyState parameter.
-   The minimum interval for creating a version of the same CMK is seven days. You can call the [DescribeKey](~~28952~~) operation to query the time when the last version of a CMK was created. The time is specified by the LastRotationDate parameter.
-   If a CMK is in a private key store, you cannot create a version for the CMK.
-   You can create a maximum of 50 versions for a CMK in the same region.

You can create a version for the CMK whose ID is `0b30658a-ed1a-4922-b8f7-a673ca9c****` by using the parameter settings provided in this topic.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=CreateKeyVersion&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateKeyVersion|The operation that you want to perform. Set the value to CreateKeyVersion. |
|KeyId|String|Yes|0b30658a-ed1a-4922-b8f7-a673ca9c\*\*\*\*|The ID of the CMK. The ID must be globally unique.

 **Note:** You can also set the value to an alias that is bound to the CMK. For more information, see [Overview of aliases](~~68522~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|KeyVersion|Struct| |The metadata of the version. |
|CreationDate|String|2019-08-02T10:38:27Z|The date and time when the version was created. The time is displayed in UTC. |
|KeyId|String|0b30658a-ed1a-4922-b8f7-a673ca9c\*\*\*\*|The ID of the CMK. The ID must be globally unique. |
|KeyVersionId|String|c0a3d5dc-0b47-4199-a050-b289349a\*\*\*\*|The ID of the version. |
|RequestId|String|b96f250a-4b75-498c-91be-22c6928f85be|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=CreateKeyVersion
&KeyId=0b30658a-ed1a-4922-b8f7-a673ca9c****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
    <KeyVersion>
        <KeyId>0b30658a-ed1a-4922-b8f7-a673ca9c****</KeyId>
        <KeyVersionId>c0a3d5dc-0b47-4199-a050-b289349a****</KeyVersionId>
        <CreationDate>2019-08-02T10:38:27Z</CreationDate>
    </KeyVersion>
    <RequestId>b96f250a-4b75-498c-91be-22c6928f85be</RequestId>
</KMS>
```

`JSON` format

```
{
        "KeyVersion": {
                "KeyId": "0b30658a-ed1a-4922-b8f7-a673ca9c****",
                "KeyVersionId": "c0a3d5dc-0b47-4199-a050-b289349a****",
                "CreationDate": "2019-08-02T10:38:27Z"
        },
        "RequestId": "b96f250a-4b75-498c-91be-22c6928f85be"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

