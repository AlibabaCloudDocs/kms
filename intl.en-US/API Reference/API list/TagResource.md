# TagResource {#reference_303902 .reference}

You can call this operation to add or modify the tags of a CMK.

## Description {#section_lm7_4hv_cnd .section}

A CMK can have more than one tag. A tag is defined by a pair of tag key and tag value.

**Note:** You can add up to 10 tags for each CMK.

For more information about tag keys and tag values, see [Tag description](#section_ut1_vco_umg).

## Request format {#section_dr8_4wg_yvi .section}

``` {#codeblock_fiz_ezz_b58}
KeyId="string"&Tags=[{ "TagKey": "string","TagValue": "string"} ]
```

## Request parameters {#section_wsc_ki3_fc2 .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|KeyId|String|Yes|external key id|The GUID of the key.|
|Tags|JSON|Yes|\[\{"TagKey": "Project", "TagValue": "Test"\}\]| One or more tags. Format: tag array. Each Tag consists of a pair of:

 -   TagKey: the tag key.
-   TagValue: the tag value.

 For more information about tag keys and tag values, see [Tag description](#section_ut1_vco_umg).

 |

## Tag description {#section_ut1_vco_umg .section}

|Parameter|Type|Required?|Example|Description|
|---------|----|---------|-------|-----------|
|TagKey|String|Yes|Project| The tag key.

 It must be 1 to 128 characters in length.

 It can contain `uppercase and lowercase letters, digits, forward slashes (/), underscores (_), hyphens (-), periods (.), plus signs (+), equal signs (=), at signs (@), and semicolons (:).`

 |
|TagValue|String|Yes|Test| The tag value.

 It can be up to 256 characters in length.

 It can contain `uppercase and lowercase letters, digits, forward slashes (/), underscores (_), hyphens (-), periods (.), plus signs (+), equal signs (=), at signs (@), and semicolons (:).`

 **Note:** Tag keys of a CMK must be unique. When you call TagResource and specify an existing tag key, the current specified tag value will overwrite the original tag value.

 |

## Sample requests {#section_1w3_d5i_l5l .section}

``` {#codeblock_v84_yv4_whg}
https://kms.cn-hangzhou.aliyuncs.com/?Action=TagResource
&KeyId=<external key id>
&Tags=<tags> 
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

