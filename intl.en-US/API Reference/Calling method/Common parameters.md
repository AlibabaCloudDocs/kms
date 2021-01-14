# Common parameters

Common request parameters must be included in all API requests.

## Common request parameters

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Format|String|No|The format in which to return the response. Valid values: JSON and XML. Default value: XML.|
|Version|String|Yes|The version number of the API. The value is in the format of YYYY-MM-DD. The current version is 2016-01-20.|
|AccessKeyId|String|Yes|The AccessKey ID provided to you by Alibaba Cloud.|
|Signature|String|Yes|The signature string of the current request. For more information about how signatures are calculated, see [Request signatures](/intl.en-US/API Reference/Calling method/Request signatures.md).|
|SignatureMethod|String|Yes|The encryption method of the signature string. Set the value to HMAC-SHA1.|
|Timestamp|String|Yes|The timestamp of the request. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. Example: 2015-12-01T12:00:00Z.|
|SignatureVersion|String|Yes|The version of the signature encryption algorithm. Set the value to 1.0.|

Examples

```
https://kms.cn-hangzhou.aliyuncs.com/?
Format=json
&Version=2016-01-20
&AccessKeyId=te****
&Signature=YlrFhyqDZQ1ThNYARrv3Ptaxqf****
&SignatureMethod=HMAC-SHA1
&Timestamp=2016-03-25T09:36:58Z
&SignatureVersion=1.0
            
```

## Common response parameters

Every response returns a unique request ID regardless of whether the call is successful.

Examples

`XML` format

```
<KMS>
  <RequestId>348d9445-e39a-4d80-907d-298cc6c94447</RequestId>
  <!-Return Result Data-->
</KMS>
            
```

`JSON` format

```
{
  "RequestId": "284b2b80-9b17-4546-a093-adfbae512a54"
}
            
```

