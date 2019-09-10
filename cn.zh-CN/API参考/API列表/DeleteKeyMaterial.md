# DeleteKeyMaterial {#concept_68623_zh .concept}

删除已导入的密钥材料。

-   此操作不会删除其对应的主密钥（CMK）。
-   如果 CMK 处于**待删除**状态，删除密钥材料不会改变密钥状态和预计删除时间；如果密钥不是处于**待删除**状态，删除密钥材料会使得密钥状态变更为**等待导入**。
-   删除密钥材料后，可以重新导入密钥材料，但必须与之前的密钥材料相同。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|CMK 的全局唯一标识符。|

## 返回参数 { .section}

|名称|类型|描述|
|RequestId|String|本次请求的 ID。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DeleteKeyMaterial
&KeyId=<external key id>
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
        "RequestId": "4162a6af-bc99-40b3-a552-89dcc8aaf7c8"
}

```

 `XML` 格式

```
//xml response
<KMS>
  <RequestId>4162a6af-bc99-40b3-a552-89dcc8aaf7c8</RequestId>
</KMS>

```

