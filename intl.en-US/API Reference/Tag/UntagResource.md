# UntagResource

Detaches tags from a customer master key \(CMK\), secret, or certificate.

In this example, the tags whose tag keys are tagkey1 and tagkey2 are detached from the CMK whose ID is `08c33a6f-4e0a-4a1b-a3fa-7ddf****`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=UntagResource&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UntagResource|The operation that you want to perform. Set the value to UntagResource. |
|TagKeys|String|Yes|\["tagkey1","tagkey2"\]|One or more tag keys. Separate multiple tag keys with commas \(,\).

 You need to specify only the tag keys, not the tag values.

 Each tag key must be 1 to 128 bytes in length. |
|KeyId|String|No|08c33a6f-4e0a-4a1b-a3fa-7ddf\*\*\*\*|The ID of the CMK. The ID must be globally unique.

 **Note:** You can set only one of the KeyId, SecretName, and CertificateId parameters. |
|SecretName|String|No|MyDbC\*\*\*\*|The name of the secret.

 **Note:** You can set only one of the KeyId, SecretName, and CertificateId parameters. |
|CertificateId|String|No|770dbe42-e146-43d1-a55a-1355db86\*\*\*\*|The ID of the certificate.

 **Note:** You can set only one of the KeyId, SecretName, and CertificateId parameters. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|4162a6af-bc99-40b3-a552-89dcc8aaf7c8|The ID of the request. |

## Examples

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=UntagResource
&KeyId=08c33a6f-4e0a-4a1b-a3fa-7ddf****
&TagKeys=["tagkey1","tagkey2"]
&<Common request parameters>|
```

Sample success responses

`XML` format

```
<KMS>
    <RequestId>4162a6af-bc99-40b3-a552-89dcc8aaf7c8</RequestId>
</KMS>
```

`JSON` format

```
{
    "RequestId": "4162a6af-bc99-40b3-a552-89dcc8aaf7c8"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

