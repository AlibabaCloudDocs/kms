# Signature {#concept_69009_zh .concept}

When you send HTTP requests to Alibaba Cloud, you sign the requests so that Alibaba Cloud can identify who sent them. You sign requests with your AccessKey, which consists of an AccessKey ID and AccessKey secret. You can apply for an AccessKey for your primary account and manage it on our official site.

## Signature process {#section_cy1_yjp_kfb .section}

1.  Create a canonical request.
    -   Sort the parameter names by character code point in ascending order. The parameters to sort include the common request parameters and the parameter of the API to call.

        **Note:** When you submit a request using the GET method, these parameters are the parameters part of the request URI "?" and connected by “&”\).

    -   Encode \(URL\) the name and value of each request parameter. Use the UTF-8 character set for coding. The coding rules are:
        -   Uppercase and lowercase letters, numbers, hyphens \(-\), underscores \(\_\), periods \(.\), and tildes \(~\) need not be encoded.
        -   Other characters are encoded as "%XY", where XY is the hexadecimal representation of the character in ASCII. The double quotation mark \("\) is coded as %22
        -   An English space \( \) is encoded as %20 rather than the plus sign \(+\).

            **Note:** Generally, libraries that support URL encoding \(e.g. Java’s java.net.URLEncoder\) are all encoded according to the rules for the “application/x-www-form-urlencoded” MIME type. If this encoding method is used, replace the plus signs \(+\) in the encoded strings with %20, the asterisks \(\*\) with %2A, and change %7E back to the tilde \(~\) to conform to the encoding rules described above.

    -   Connect the encoded parameter names and values with the English equals sign \(=\).
    -   Then, order the parameter name and value pairs connected by equals signs in alphabetical order and connect them with the & symbol to produce the Canonicalized Query String.

        Use the Canonicalized Query String obtained in the preceding step to construct the string for signature calculation according to the following rules:

        ```
        StringToSign=
        HTTPMethod + “&” +
        percentEncode(“/”) + ”&” +
        percentEncode(CanonicalizedQueryString)
        
        ```

        HTTPMethod: indicates the HTTP method used for request submission, for example, GET. - percentEncode\(“/”\): the coded value for the character “/“ according to the URL encoding rules described above, namely, “%2F”.

        percentEncode\(CanonicalizedQueryString\) indicates the encoded string of the Canonicalized Query String constructed in step 1.b, produced by following the URL encoding rules described in 1.b.

2.  Use the preceding signature sting to calculate the signature’s HMAC value based on [RFC2104](http://www.ietf.org/rfc/rfc2104.txt) definitions. Note: The Key used for signature calculation is the Access Key Secret held by the user added with a "&" character \(ASCII:38\), and the SHA1 hashing algorithm is used.
3.  According to Base64 encoding rules, encode the preceding HMAC value, which gives you the signature value.
4.  Add the obtained signature value to the request parameters as the “Signature” parameter, which completes the request signing process.

    **Note:** Note: When the obtained signature value is submitted to the KMS server as the final request parameter value, the value will be URL encoded like other parameters according to RFC3986 rules.


## Examples { .section}

Take `CreateKey` as an example, the request URL before signature is:

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=CreateKey
&SignatureVersion=1.0
&Format=json
&Version=2016-01-20
&AccessKeyId=testid
&SignatureMethod=HMAC-SHA1
&Timestamp=2016-03-28T03:13:08Z

```

`CanonicalizedQueryString` is:

```
AccessKeyId=testid&Action=CreateKey&Format=json&SignatureMethod=HMAC-SHA1&SignatureVersion=1.0&Timestamp=2016-03-28T03%3A13%3A08Z&Version=2016-01-20

```

`StringToSign` is:

```
GET&%2F&AccessKeyId%3Dtestid&Action%3DCreateKey&Format%3Djson&SignatureMethod%3DHMAC-SHA1&SignatureVersion%3D1.0&Timestamp%3D2016-03-28T03%253A13%253A08Z&Version%3D2016-01-20

```

If the Access Key ID is `testid`, the Access Key Secret is `testsecret`, and the Key used for HMAC calculation is `testsecret&`, the calculated signature value is:

```
s/OdVWMTmNGagvWlljdAJ7Itsew=

```

The signed request URL is \(with the Signature parameter added\):

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=CreateKey
&SignatureVersion=1.0
&Format=json
&Version=2016-01-20
&AccessKeyId=F585********APMU
&SignatureMethod=HMAC-SHA1
&Timestamp=2016-03-28T03:13:08Z
&Signature=41wk2SSX1GJh7fwnc5eqOfiJPFg%3D


```

