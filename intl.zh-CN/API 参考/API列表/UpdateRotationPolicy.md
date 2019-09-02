# UpdateRotationPolicy {#concept_1926042 .concept}

更新密钥轮转策略。

如果开启自动轮转，将在上一次轮转时间加上轮转周期天数后，自动创建一个新的密钥版本，并将它设置为主版本。下列情况不允许配置自动轮转策略：

-   指定的主密钥为云产品托管的默认密钥。
-   指定的主密钥为用户自带密钥（外部导入到KMS的密钥）。
-   指定的主密钥处于Enabled之外的状态。

## 请求参数 {#section_hcv_5g7_cvp .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|主密钥的全局唯一标识符|
|EnableAutoRotation|Boolean|是|是否开启自动密钥轮转。 有效值：true或false|
|RotationIntervalInDays|Integer|否|自动轮转周期（天数）。 有效值范围：\[7,730\]。 **说明：** 

-   当EnableAutoRotation为true时必须设置此参数。
-   当EnableAutoRotation为false时忽略此参数。

 |

## 返回参数 {#section_vba_z04_x5i .section}

|名称|类型|描述|
|RequestId|String|本次请求的ID|

## 示例 {#section_r1d_43o_hs8 .section}

请求示例

``` {#codeblock_w0m_ewo_ofk}
https://kms.cn-hangzhou.aliyuncs.com/?Action=UpdateRotationPolicy
&KeyId=<key id>
&EnableAutoRotation=true
&RotationIntervalInDays=30
&<其他公共参数>
```

返回示例

`JSON`格式

``` {#codeblock_8k6_52v_04k}
//json response
{
        "RequestId": "80b4eac8-9f51-452a-a859-0c9b06b283c1"
}
```

`XML`格式

``` {#codeblock_rl6_0ya_icx}
//xml response
<KMS>
        <RequestId>b0ae52a2-33a4-43de-b68c-849f81d09f5d</RequestId>
</KMS>
```

