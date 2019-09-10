# DescribeRegions {#concept_54560_zh .concept}

查询当前账户的可用地域列表。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|Action|String|是|操作接口名。取值：DescribeRegions。|

## 返回参数 { .section}

|名称|类型|描述|
|RegionId|String|可用区 ID。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DescribeRegions
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
        "Regions": {
                "Region": [
                        {
                                "RegionId": "cn-beijing"
                        },
                        {
                                "RegionId": "cn-hangzhou"
                        }
                ]
        },
        "RequestId": "815240e2-aa37-4c26-9cca-05d4df3e8fe6"
}

```

 `XML` 格式

```
//xml response
<KMS>
	<Regions>
		<Region>
			<RegionId>cn-beijing</RegionId>
		</Region>
		<Region>
			<RegionId>cn-hangzhou</RegionId>
		</Region>
	</Regions>
	<RequestId>815240e2-aa37-4c26-9cca-05d4df3e8fe6</RequestId>
</KMS>

```

