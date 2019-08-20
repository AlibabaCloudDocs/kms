# Common parameters {#concept_69007_zh .concept}

Common request parameters are used in each API.

## Common request parameters {#section_zf5_djp_kfb .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Format|String|No|The format of the response text. JSON and XML are supported. The default format is XML.|
|Version|String|Yes|The API version in the format YYYY-MM-DD. The current version is 2016-01-20.|
|AccessKeyId|String|Yes|An alphanumeric token issued by Alibaba Cloud for user authentication.|
|Signature|String|Yes|Signing requests. For more information, see [Signature](intl.en-US/API Reference/Calling method/Signature.md#).|
|SignatureMethod|String|Yes|The hash algorithm to create the request signature. HMAC-SHA1 is used.|
|Timestamp|String|Yes|The time stamp of the request. The date and time at which a request is signed, in the format YYYY-MM-DDThh:mm:ssZ. Example: 2014-05-26T12:00:00Z|
|SignatureVersion|String|Yes|The signature version used to sign a request. The current version is 1.0.|

**Example**

```
https://kms.cn-hangzhou.aliyuncs.com/?
Format=json
&Version=2016-01-20
&AccessKeyId=testid
&Signature=YlrFhyqDZQ1ThNYARrv3Ptaxqf****
&SignatureMethod=HMAC-SHA1
&Timestamp=2016-03-25T09:36:58Z
&SignatureVersion=1.0

```

## Common response parameters { .section}

Each time you send an API request, a unique RequestId is returned, whether the request is successful or not.

**Example**

 `XML` example

```
<KMS>
<RequestId>348d9445-e39a-4d80-907d-298cc6c94447</RequestId>
<!—Returned results-->
</KMS>

```

 `JSON` example

```
{
"RequestId": "284b2b80-9b17-4546-a093-adfbae512a54"
}

```

