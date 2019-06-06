# ListResourceTags {#reference_303904 .reference}

You can call this operation to list the tags of a CMK.

## Request format {#section_dr8_4wg_yvi .section}

``` {#codeblock_fiz_ezz_b58}
KeyId="string"
```

## Request parameters {#section_wsc_ki3_fc2 .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|KeyId|String|Yes|key id|The GUID of the key.|

## Sample requests {#section_1w3_d5i_l5l .section}

``` {#codeblock_v84_yv4_whg}
https://kms.cn-hangzhou.aliyuncs.com/?Action=ListResourceTags
&KeyId=<key id>
&<Common request parameters>
```

## Response parameters {#section_1mx_9zy_w2g .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|4162a6af-bc99-40b3-a552-89dcc8aaf7c8|The request ID.|
|TagKey|String|Project|The tag key.|
|TagValue|String|Test|The tag value.|

## Sample responses {#section_pj4_dkc_jiy .section}

JSON format

``` {#codeblock_6iw_t7q_e42}
{
    "RequestId": "4162a6af-bc99-40b3-a552-89dcc8aaf7c8",
    "Tags": {
            "Tag": [
                {
                    "KeyId": "33caea95-c3e5-4b3e-a9c6-cec76e4eaf83",
                    "TagKey": "Project",
                    "TagValue": "Test"
                }
            ]
        }
}
```

XML format

``` {#codeblock_xis_t6p_fgx}
<KMS>
        <RequestId>0f900dad-c747-4170-9962-1bfb6b31436b</RequestId> 
        <Tags>
            <Tag>
                <KeyId>33caea95-c3e5-4b3e-a9c6-cec76e4eaf83</KeyId> 
                <TagKey>Project</TagKey> 
                <TagValue>Test</TagValue> 
            </Tag> 
        </Tags> 
</KMS> 
```

