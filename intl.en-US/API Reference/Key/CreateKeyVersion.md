# CreateKeyVersion

Creates a new version for the CMK.

This operation is available only for asymmetric CMKs and only when the CMK is in the Enabled state. The minimum interval at which a key version is created is seven days. If you call this operation within seven days after the creation of the last key version, the error code **Rejected.UnsupportedOperation**is returned. The creation date of the last key version is specified by the **LastRotationDate** parameter. Each user can hold up to 50 asymmetric key versions in each region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=CreateKeyVersion&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateKeyVersion|The operation that you want to perform. Set the value to CreateKeyVersion. |
|KeyId|String|Yes|0b30658a-ed1a-4922-b8f7-a673ca9c\*\*\*\*|The globally unique ID of the CMK. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|b96f250a-4b75-498c-91be-22c6928f85be|The ID of the request. |
|KeyVersion|Struct| |The metadata of the newly created key version. |
|KeyId|String|0b30658a-ed1a-4922-b8f7-a673ca9c\*\*\*\*|The globally unique ID of the CMK. |
|KeyVersionId|String|c0a3d5dc-0b47-4199-a050-b289349a\*\*\*\*|The ID of the newly created key version. |
|CreationDate|String|2019-08-02T10:38:27Z|The date and time the new key version was created. The time is displayed in UTC. |

## Examples

Sample requests

```
https://[Endpoint]/?Action=CreateKeyVersion
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

