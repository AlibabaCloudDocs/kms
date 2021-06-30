# Disable, revoke, or delete a certificate

You can use Certificates Manager to manage private keys and certificates as well as generate and verify signatures. If you no longer need a certificate, you can disable, revoke, or delete the certificate.

Your certificate is enabled.

## Disable a certificate

If you temporarily do not need a certificate, you can disable it. After a certificate is disabled, its information is retained. You can enable the certificate again if you require it later.

1.  Log on to the [Key Management Service \(KMS\) console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region in which you want to create a certificate.

3.  In the left-side navigation pane, click **Certificate**.

4.  Find the certificate that you want to disable and click **Disable** in the **Operating** column.

5.  In the Disable certificate message, click **OK**.

    **Note:** You can click **Enable** in the **Operating** column to enable the certificate again.


## Revoke a certificate

If a certificate is revoked by the certificate authority \(CA\), you can change the status of the certificate to **Revoked** in the KMS console. After the certificate is revoked, its information is retained. You can view the information later. However, you cannot enable or disable the certificate.

1.  Find the certificate for which you want to change the status and click **Revoked** in the **Operating** column.

2.  In the Revoke certificate message, click **OK**.


## Delete a certificate

If you no longer need a certificate, you can delete it. Before you delete a certificate, make sure that the certificate is not used to generate or verify signatures.

1.  Find the certificate that you want to delete and choose **More** \> **Delete certificate** in the **Operating** column.

2.  In the Delete certificate message, click **OK**.


