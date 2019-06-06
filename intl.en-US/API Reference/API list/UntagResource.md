# UntagResource {#reference_303902 .reference}

You can call this operation to delete the specified tags of a CMK.

## Request format {#section_dr8_4wg_yvi .section}

``` {#codeblock_fiz_ezz_b58}
KeyId="string"&TagKeys=["tagkey1","tagkey2"] 
```

## Request parameters {#section_wsc_ki3_fc2 .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|KeyId|String|Yes|external key id|The GUID of the key.|
|TagsKeys|JSON|Yes|\["tagkey1","tagkey2"\]|One or more tag keys. Only the tag keys are required, and tag values are not required. Format: string array. Each string in the array must be 1 to 128 characters in length.|

## Sample requests {#section_1w3_d5i_l5l .section}

``` {#codeblock_v84_yv4_whg}
https://kms.cn-hangzhou.aliyuncs.com/?Action=UntagResource
&KeyId=<external key id>
&TagKeys=<tagkeys> 
&<Common request parameters>
```

## Response parameters {#section_1mx_9zy_w2g .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|4162a6af-bc99-40b3-a552-89dcc8aaf7c8|The request ID.|

## Sample responses {#section_pj4_dkc_jiy .section}

JSON format

``` {#codeblock_6iw_t7q_e42}
{
    "RequestId": "4162a6af-bc99-40b3-a552-89dcc8aaf7c8"
}
```

XML format

``` {#codeblock_xis_t6p_fgx}
<KMS>
  <RequestId>4162a6af-bc99-40b3-a552-89dcc8aaf7c8</RequestId>
</KMS>
```

