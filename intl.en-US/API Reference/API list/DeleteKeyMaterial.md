# DeleteKeyMaterial {#concept_68623_zh .concept}

Deletes the imported key material.

-   This operation does not cause the deletion of the specified CMK.
-   If the specified CMK is in **PendingDeletion**state, this operation does not change the CMK’s state or the scheduled deletion time. If the CMK is not in **PendingDeletion** state，it changes the CMK’s state to **PendingImport**.
-   After you delete the key material, you can reimport the same key material into the CMK. You cannot import a different key material.

## Request parameters { .section}

|Name|Type|Required|Description|
|KeyId|String|Yes|Globally unique identifier of the CMK.|

## Response parameters { .section}

|Name|Type|Description|
|RequestId|String|The ID of this request.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DeleteKeyMaterial
&KeyId=<external key id>
&<Common Request Parameters>

```

**Response example**

 `JSON` format

```
//json response
{
        "RequestId": "4162a6af-bc99-40b3-a552-89dcc8aaf7c8"
}

```

 `XML` format

```
//xml response
<KMS>
  <RequestId>4162a6af-bc99-40b3-a552-89dcc8aaf7c8</RequestId>
</KMS>

```

