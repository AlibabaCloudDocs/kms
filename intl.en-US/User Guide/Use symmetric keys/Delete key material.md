# Delete key material

After you import key material, you can directly delete the key material. In this case, the key will no longer function and the ciphertext encrypted by using the key cannot be decrypted. This topic describes how to delete key material.

Key material is imported. For information about how to import key material, see [Import key material](/intl.en-US/User Guide/Use symmetric keys/Import key material.md).

After you import key material into an external key, you can use the external key just like a normal key. The only difference is that the key material of an external key may expire and can be independently deleted. After the key material of an external key expires or is deleted, the external key can no longer be used, and the ciphertext encrypted by using this external key cannot be decrypted. After you delete the imported key material, you can re-import the same key material to make the relevant CMK available again. Therefore, we recommend that you save a copy of the key material.

## Delete key material in the KMS console

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the top navigation bar, select the region where your key resides.

3.  In the left-side navigation pane, click **Keys**.

4.  Find your key and click its alias to go to the key management page.

5.  In the **Key Material** section of the page that appears, click **Delete Key Material**. In the message that appears, click OK.

    After the key material is deleted, the key state changes from **Enabled** to **Pending Import**.


## Delete key material by using Alibaba Cloud CLI

Run the aliyun kms DeleteKeyMaterial command to call the [DeleteKeyMaterial](/intl.en-US/API Reference/Key/DeleteKeyMaterial.md) operation to delete key material.

```
aliyun kms DeleteKeyMaterial --KeyId 1339cb7d-54d3-47e0-b595-c7d3dba8****      
```

