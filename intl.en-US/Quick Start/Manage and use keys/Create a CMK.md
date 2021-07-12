# Create a CMK

This topic describes how to create a customer master key \(CMK\) in the Key Management Service \(KMS\) console. CMKs are used to encrypt data.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region where you want to create a CMK.

3.  In the left-side navigation pane, click **Keys**.

4.  Click **Create Key**.

5.  In the Create Key dialog box, configure the parameters based on your business requirements.

    |Parameter|Description|
    |---------|-----------|
    |**KeyStore**|The key store where you want to store the CMK. For more information, see [Overview](/intl.en-US/Key Service/Private Key Store/Overview.md). |
    |**Key Spec**|The type of the CMK. Valid values:    -   Symmetric:
        -   Aliyun\_AES\_256
        -   Aliyun\_SM4
    -   Asymmetric:
        -   RSA\_2048
        -   RSA\_3072
        -   EC\_P256
        -   EC\_P256K
        -   EC\_SM2
**Note:** Aliyun\_SM4 and EC\_SM2 types are supported only for regions in mainland China where managed hardware security modules \(HSMs\) are used. |
    |**Purpose**|The purpose of the CMK. Valid values:    -   Encrypt/Decrypt: encrypts or decrypts data.
    -   Sign/Verify: generates or verifies a digital signature. |
    |**Alias Name**|The alias of the CMK, which helps identify the CMK. Aliases are optional to CMKs. For more information, see [Overview](/intl.en-US/Key Service/Manage aliases/Overview.md). |
    |**Protection Level**|The protection level of the CMK. Valid values:    -   Software: The CMK is protected by using a software module.
    -   Hsm: The CMK is managed in an HSM, which is dedicated to safeguard the CMK. |
    |**Description**|The description of the CMK.|
    |**Rotation Period**|The interval of automatic rotation. Valid values:    -   30 Days
    -   90 Days
    -   180 Days
    -   365 Days
    -   Disable: Automatic rotation is disabled.
    -   Customize: You can customize an interval that ranges from 7 days to 730 days.
**Note:** You can specify this parameter only when you set the Key Spec parameter to Aliyun\_AES\_256 or Aliyun\_SM4. |

6.  Click **Advanced** and set the **Key Material Source** parameter.

    **Note:** The Advanced option appears only when you set the Key Spec parameter to Aliyun\_AES\_256 or Aliyun\_SM4.

    -   **Alibaba Cloud KMS**: KMS generates key material.
    -   **External**: You must import key material from an external source. For more information, see [Import key material](/intl.en-US/Key Service/Key type/Use symmetric keys/Import key material.md).

        **Note:** If you select External, you must also select **I understand the implications of using the external key materials key**.

7.  Click **OK**.

    After the CMK is created, you can view its detailed information, such as the CMK ID, status, and protection level.


