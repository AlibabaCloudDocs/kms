# Responses

API responses use the HTTP response format where a 2xx status code indicates a successful call and a 4xx or 5xx status code indicates a failed call.

**Note:**



-   Responses can be returned only in the JSON format.
-   If you make an API request by using third-party tools, you can customize the response format in the request parameters.
-   This topic uses line feeds in the sample responses to enhance readability.

## Sample success responses

`JSON` format

```
{
    "RequestId": "4C467B38-3910-447D-87BC-AC049166F216",
    /* Return Result Data */
}
```

## Sample error responses

If an error occurs during an API call, response data is not returned. You can troubleshoot an error based on error codes specific to an operation and error codes described in the [Common errors](#section_69008_03) section of this topic.

If an error occurs during an API call, the HTTP status code, error code, error message, and ID of the request are returned in the response. If you cannot troubleshoot the error based on the error code and error message, you can provide Alibaba Cloud technical support with the ID of the request to locate the request log.

`XML` format \(an expired request\)

```
<KMS>
     <HttpStatus>400</HttpStatus>
     <Code>IllegalTimestamp</Code>
     <Message>The input parameter "Timestamp" that is mandatory for processing this request is not supplied. </Message>
     <RequestId>3b237773-bc2c-4bea-95fc-319a1a5baa68</RequestId>
</KMS>
```

`JSON` format \(an expired request\)

```
{
     "HttpStatus": 400,
     "Code": "IllegalTimestamp",
     "Message": "The input parameter \"Timestamp\" that is mandatory for processing this request is not supplied.",
     "RequestId": "e85db688-a2d3-44ca-9790-4259f59e90d8"
}
```

## Common errors

|Error code|Error message|HTTP status code|
|:---------|:------------|:---------------|
|InternalFailure|Internal Failure.|500|
|ServiceUnavailableTemporary|Service Unavailable Temporary.|503|
|InvalidAccessKeyId.NotFound|The AccessKey ID provided does not exist in our records.|404|
|Forbidden.KeyNotFound|The specified Key is not found.|404|
|Forbidden.KeyVersionNotFound|The specified Key version is not found.|404|
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
|Unsupported.ProtectionLevel|This protection level is not valid for this region|400|
|Rejected.StateModifiedFailed|Keystate modified failed.|409|
|Rejected.Disabled|The request was rejected because the key state is Disabled.|409|
|Rejected.PendingDeletion|The request was rejected because the key state is PendingDeletion.|409|
|Rejected.PendingImport|The request was rejected because the key state is PendingImport.|409|

