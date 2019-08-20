# DescribeRegions {#concept_54560_zh .concept}

Returns available regions for the specified account.

## Request parameters { .section}

|Name|Type|Required|Description|
|Action|String|Yes|Action interface name. Value: DescribeRegions.|

## Response parameters { .section}

|Name|Type|Description|
|RegionId|String|Region ID.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DescribeRegions
&<Common Request Parameters>

```

**Response example**

 `JSON` format

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

 `XML` format

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

