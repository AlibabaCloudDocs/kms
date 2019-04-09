# Response structure {#concept_69008_zh .concept}

After you make an API request, an HTTP status code is returned. 2xx indicates that the request has succeeded; 4xx or 5xx indicates that an error occurred while processing the request. The response text is JSON formatted.

If you make the API request by using tools that are not provided by Alibaba Cloud, you can customize the response format in the request parameters.

In the example responses we present as follows, we use line breaks to separate the original whole line of text for readability.

## Successful response example {#section_w25_vmp_kfb .section}

`XML` example:

```
<? xml version="1.0" encoding="UTF-8"? > 
<! --Result Root Node-->
<InterfaceName+Response>
    <! -- Return Request Tag -->
	<RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
    <! -- Return Result Data -->
</InterfaceName+Response>
			
```

`JSON` example:

```
{
    "RequestId": "4C467B38-3910-447D-87BC-AC049166F216",
    /* Return Result Data */
}
			
```

## Unsuccessful response example { .section}

After an error is encountered in an interface call, no result data will be returned. The caller can locate the error cause according to the error code and [Public error codes](#) corresponding to each interface.

When an error occurs in a call, the HTTP request will return an HTTP status code of 4xx or 5xx. The returned message body contains the specific error code and error message. The message body also contains a globally unique RequestId and the requested HostId. If the caller cannot find the cause of the error, he can contact AliCloud customer service and provide the HostId and RequestId to help us solve the problem as quickly as possible.

`XML` example \(request expiration\)

```
<KMS>
<HttpStatus>400</HttpStatus>
<Code>IllegalTimestamp</Code>
<Message>The input parameter "Timestamp" that is mandatory for processing this request is not supplied. </Message>
<RequestId>3b237773-bc2c-4bea-95fc-319a1a5baa68</RequestId>
 </KMS>
			
```

`JSON` example \(request expiration\)

```
{
"HttpStatus": 400
"Code": "IllegalTimestamp"
"Message": "The input parameter "Timestamp" that is mandatory for processing this request is not supplied."
"RequestId": "e85db688-a2d3-44ca-9790-4259f59e90d8"
}
			
```

## Public error codes {#section_69008_03 .section}

|Error code|Error message|HTTP status code|
|:---------|:------------|:---------------|
|InternalFailure|Internal Failure.|500|
|SerivceUnavailableTemporary|Service Unavailable Temporary.|503|
|InvalidAccessKeyId.NotFound|The AccessKey ID provided does not exist in our records.|404|
|Forbidden.KeyNotFound|The specified Key is not found.|404|
|Forbidden.AliasNotFound|The specified Alias is not found.|404|
|Forbidden.NoPermission|This operation is forbidden by permission system.|403|
|Forbidden.AccessKey|This AccessKey is not enabled.|403|
|UnsupportedHTTPMethod|This http method is not supported.|403|
|Forbidden.UbsmsInvalidUserid|Userid Invalid For Ubsms.|403|
|Forbidden.UbsmsInvalidBid|Your account partner does not have KMS Service.|403|
|Forbidden.KmsServiceNotEnabled|Kms service is not Enabled for current user. Please get access permission first.|403|
|Forbidden.ProhibitedByRiskControl|Current user is Prohibited By Risk Control.|403|
|Forbidden.InDebtOverdue|Current user is indebted Overdue.|403|
|Forbidden.InDebt|Current user is indebted.|403|
|ParseRequestParameterException|Server parse parameters exception. Please check your input params.|400|
|MissingParameter|The parameter "< parameter name \>" is needed but not provided.|400|
|InvalidParameter|The specified parameter "< parameter name \>" is not valid.|400|
|IncompleteSignature|The request signature does not conform to Alibaba Cloud standards.|400|
|IllegalTimestamp|The input parameter "Timestamp" that is required for processing this request is not supplied.|400|
|Rejected.LimitExceeded|The request was rejected because user create resource limit was exceeded.|400|
|AliasAlreadyExists|AliasName Already Exists.|400|
|InvalidKeyMaterial|key material is invalid.|400|
|InvalidImportToken|import token is invalid.|400|
|ExpiredImportToken|import token is expired.|400|
|Unsupported.Origin|This key origin is not valid for this api.|400|
|Unsupported.Alias|Alias is not valid for this api.|400|
|Rejected.StateModifiedFailed|Keystate modified failed.|409|
|Rejected.Disabled|The request was rejected because the key state is Disabled.|409|
|Rejetced.PendingDeletion|The request was rejected because the key state is PendingDeletion.|409|
|Rejected.PendingImport|The request was rejected because the key state is PendingImport.|409|

