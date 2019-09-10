# UpdateKeyDescription {#concept_1942029 .concept}

更新主密钥的描述信息。

将主密钥的描述信息（[KeyMetadata](intl.zh-CN/API 参考/API列表/DescribeKey.md#section_28952_03)中的Description属性）替换为用户传入的值。使用此API可以对密钥的描述信息进行添加、变更、删除操作。

## 请求参数 {#section_hxx_nk3_qai .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|主密钥（CMK）的全局唯一标识符|
|Description|String|是|CMK的描述性信息，通常用于描述CMK的用途，例如CMK保护的数据类型、可使用CMK的应用等。|

## 返回参数 {#section_vhe_bjq_c8z .section}

|名称|类型|描述|
|RequestId|String|当前请求的标志符|

## 示例 {#section_cws_131_vi7 .section}

请标志符求示例

``` {#codeblock_519_6hb_vsv}
https://kms.cn-hangzhou.aliyuncs.com/?Action=UpdateKeyDescription
&KeyId=<cmkid>
&Description=<your key description>
&<公共请求参数>
```

返回示例

`JSON`格式

``` {#codeblock_wbn_4l2_2wz}
//json response
{
    "RequestId": "475f1620-b9d3-4d35-b5c6-3fbdd941423d"
}
```

`XML`格式

``` {#codeblock_cdd_aky_1cq}
//xml response
<KMS>
    <RequestId>475f1620-b9d3-4d35-b5c6-3fbdd941423d</RequestId>
</KMS>     
```

