# Manage CMKs {#concept_qpd_15s_xgb .task}

You can use Key Management Service \(KMS\) to create and manage customer master keys \(CMKs\), and then use CMKs to encrypt data.

## Create a CMK {#section_yhn_otu_mvs .section}

Follow these steps to create a CMK:

1.  Log on to the [KMS console](https://partners-intl.console.aliyun.com/#/kms).
2.  In the upper-left corner of the page, click **Create Key**.
3.  In the Create Key dialog box, enter an **alias** and **description**.
4.  Click **Advanced**, and then select a **key material source**. 
    -   **Alibaba Cloud KMS**: use KMS to generate the key material.
    -   **External**: manually import the key material. For more information, see [Import key material](../../../../reseller.en-US/User Guide/Import key material.md#).
5.  Click **OK**.

**Note:** After the CMK is created, click **More** to check the CMK ID, status, protection level, and other detailed information.

## Disable a CMK {#section_6pl_5dc_o3w .section}

By default, newly created CMKs are enabled. You cannot use disabled CMKs to encrypt and decrypt data. Follow these steps to disable a CMK:

1.  In the key list, find the CMK that you want to disable.
2.  Click **Disable** in the Actions column.
3.  Click **OK**.

## Schedule a key deletion task {#section_bpi_asr_rya .section}

After a CMK is deleted, it cannot be recovered. Content and ciphertext data keys encrypted by using this CMK cannot be decrypted. Therefore, to prevent you from deleting CMKs by mistake, KMS only allows you to schedule key deletion tasks. You cannot directly delete CMKs. We recommend that you disable a CMK instead of deleting it.

1.  In the key list, find the CMK that you want to delete.
2.  Choose **More** \> **Schedule Key Deletion**.
3.  In the Schedule Key Deletion dialog box, enter the number of days after which the CMK is going to be deleted. Valid values: 7 to 30 days.
4.  Click **OK**.

**Note:** 

-   A CMK pending for deletion cannot be used to encrypt data, decrypt data, or generate data keys.
-   You can click **Cancel Key Deletion** to cancel a scheduled key deletion task.

