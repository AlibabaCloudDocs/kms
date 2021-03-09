# Create a CMK

This topic shows you how to use Key Management Service \(KMS\) to create customer master keys \(CMKs\). CMKs are used to encrypt data.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region in which you want to create a CMK.

3.  In the left-side navigation pane, click **Keys**.

4.  Click **Create Key**.

5.  In the Create Key dialog box, set the parameters as required.

    |Parameter|Description|
    |---------|-----------|
    |**KeyStore**|A key store is a security domain that is used to store the CMK of KMS. For more information, see [t2045267.md\#]().|
    |**Key Spec**|The type of the CMK. Valid values:    -   Symmetric keys:
        -   Aliyun\_AES\_256
        -   Aliyun\_SM4
    -   Asymmetric keys:
        -   RSA\_2048
        -   EC\_P256
        -   EC\_P256K
        -   EC\_SM2
**Note:** Aliyun\_SM4 and EC\_SM2 types are used only in mainland China regions where managed hardware security modules \(HSMs\) are available. |
    |**Purpose**|    -   Encrypt/Decrypt: The purpose of the CMK is to encrypt or decrypt data.
    -   Sign/Verify: The purpose of the CMK is to generate or verify a digital signature. |
    |**Alias Name**|The optional identifier of the CMK. For more information, see [Overview](/intl.en-US/Key Service/Manage aliases/Overview.md).|
    |**Protection Level**|    -   Software: Use a software module to protect the CMK.
    -   Hsm: Manage the CMK in an HSM, which is dedicated hardware that safeguards the CMK. |
    |**Description**|The description of the CMK.|
    |**Rotation Period**|The interval of automatic rotation. Valid values:    -   30 Days
    -   90 Days
    -   180 Days
    -   365 Days
    -   Disable: Automatic rotation is disabled.
    -   Customize: Customize an interval that ranges from 7 days to 730 days.
**Note:** You can specify this parameter only if the Key Spec parameter is set to Aliyun\_AES\_256 or Aliyun\_SM4. |

6.  Click **Advanced** and set the **Key Material Source** parameter.

    -   **Alibaba Cloud KMS**: Use KMS to generate key material.
    -   **External**: Import key material from an external source. For more information about how to import key material, see [Import key material](/intl.en-US/Key Service/Key type/Use symmetric keys/Import key material.md).

        **Note:** If you select External, you must also select the check box for **I understand the implications of using the external key materials key**.

7.  Click **OK**.

    After the CMK is created, you can view its detailed information, such as the CMK ID, status, and protection level.


