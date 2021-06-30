# Common parameters

This topic describes the parameters that are common to all API requests and responses.

## Common request parameters

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Format|String|No|The response format. Valid values:-   JSON \(default\)
-   XML |
|Version|String|Yes|The version number of the API. The value must be in the YYYY-MM-DD format. Set the value to 2016-01-20.|
|AccessKeyId|String|Yes|The AccessKey ID provided to you by Alibaba Cloud.|
|Signature|String|Yes|The signature string of the current request.|
|SignatureMethod|String|Yes|The encryption method of the signature string. Set the value to HMAC-SHA1.|
|Timestamp|String|Yes|The timestamp of the request. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. For example, use 2013-01-10T12:00:00Z to indicate January 10, 2013, 20:00:00 \(UTC+8\). |
|SignatureVersion|String|Yes|The version of the signature encryption algorithm. Set the value to 1.0.|

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=CreateKey
Format=json
&Version=2016-01-20
&AccessKeyId=te****
&Signature=YlrFhyqDZQ1ThNYARrv3Ptaxqf****
&SignatureMethod=HMAC-SHA1
&Timestamp=2016-03-25T09:36:58Z
&SignatureVersion=1.0          
```

## Common response parameters

Responses can be returned in either the JSON or XML format. You can specify the response format in the request. The default response format is JSON. Every response returns a unique RequestId regardless of whether the call is successful.

-   An HTTP `2xx` status code indicates a successful call.
-   An HTTP `4xx` or `5xx` status code indicates a failed call.

Sample responses

-   XML format

    ```
    <?xml version="1.0" encoding="utf-8"?> 
        <!--Result Root Node-->
        <KMS>
            <!--Return Request Tag-->
            <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
            <!--Return Result Data-->
        </KMS>                        
    ```

-   JSON format

    ```
    {
        "RequestId":"4C467B38-3910-447D-87BC-AC049166F216"
        /*Return Result Data*/
    }
    ```


