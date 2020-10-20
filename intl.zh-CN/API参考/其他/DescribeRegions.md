# DescribeRegions

调用DescribeRegions接口查询当前账号的可用地域列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=DescribeRegions&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeRegions|要执行的操作，取值：DescribeRegions。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Regions|Array of Region| |地域。 |
|Region| | | |
|RegionId|String|cn-hangzhou|地域ID。 |
|RequestId|String|815240e2-aa37-4c26-9cca-05d4df3e8fe6|请求ID。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DescribeRegions
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
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

`JSON` 格式

```
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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

