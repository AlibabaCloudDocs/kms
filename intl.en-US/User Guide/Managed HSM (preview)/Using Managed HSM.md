# Using Managed HSM {#concept_1216443 .concept}

This topic describes how to create and use keys through Managed HSM.

## Enable free-trial version of Managed HSM {#section_tgc_fqk_dda .section}

You can contact your pre-sales or after-sales consultant to enable the free-trial version of Managed HSM.

## Create a key in Managed HSM {#section_fxo_mgd_9yl .section}

You can only use Managed HSM in some regions. For more information about supported regions, see [Supported regions](reseller.en-US/User Guide/Managed HSM (preview)/Overview.md#section_9br_g7q_yb4).

Create a key in the console

1.  Log on to the [KMS console](https://partners-intl.console.aliyun.com/#/kms/).
2.  Select a region in the upper-left corner of the page. Click **Create Key**.
3.  Select **HSM** from the **Protection Level** drop-down list.
4.  Enter a description and click **OK**.

After a key is created, its **Protection Level** is displayed on the **Key Details** and **Keys** pages.

Create a key by using Alibaba Cloud CLI

`aliyun kms CreateKey --ProtectionLevel HSM --Description "Key1 in Managed HSM"`

The protection level of the key is displayed in the output after the key is created or in the output of DescribeKey called by using Alibaba Cloud CLI. Example:

``` {#codeblock_p83_ja7_4ru .language-json}
{
  "KeyMetadata": {
    "CreationDate": "2019-07-04T13:14:15Z",
    "Description": "Key1 in Managed HSM",
    "KeyId": "1234abcd-12ab-34cd-56ef-12345678****",
    "KeyState": "Enabled",
    "KeyUsage": "ENCRYPT/DECRYPT",
    "DeleteDate": "",
    "Creator": "111122223333",
    "Arn": "acs:kms:cn-hongkong:111122223333:key/1234abcd-12ab-34cd-56ef-12345678****",
    "Origin": "Aliyun_KMS",
    "MaterialExpireTime": "",
    "ProtectionLevel": "HSM"
  },
  "RequestId": "8eaeaa8b-4491-4f1e-a51e-f95a4e54620c"
}
```

## Import external keys to Managed HSM {#section_duf_2vy_qrn .section}

You can also import keys from user-created key infrastructure to Managed HSM. You only need to set **Protection Level** to **HSM** in the first step of the [import key material](import key materialEN-US_TP_22680.dita#concept_68523_zh) process. This step is to **create external keys**. Keep the remaining steps unchanged.

The actions on the Alibaba Cloud side:

-   When you call GetParametersForImport, Alibaba Cloud generates a key pair for importing external keys in Managed HSM based on the **HSM** protection level, and returns the public key of the key pair.
-   When you call ImportKeyMaterial, Alibaba Cloud imports the encrypted external key material to Managed HSM, and obtains the key material by unwrapping the HSM key. The imported plaintext key material will never be exported.

## Manage and use keys {#section_y5c_hj3_m69 .section}

All management and cryptographic features supported by KMS are applicable to keys created in Managed HSM. Specifically, you can:

-   Enable and disable keys.
-   Manage key lifecycle.
-   Manage key aliases.
-   Manage key tags.
-   Call key operations.

## Integration with other cloud products {#section_v5u_cnm_a5y .section}

Keys created in Managed HSM can be used in other cloud products such as ECS, RDS, and OSS through standard APIs of KMS, to protect your native Alibaba Cloud data. In this case, cloud products must support server-side encryption by using custom keys. You only need to select keys created in Managed HSM when configuring CMKs for server-side encryption on cloud products.

