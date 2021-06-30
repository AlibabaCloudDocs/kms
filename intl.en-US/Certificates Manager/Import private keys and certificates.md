# Import private keys and certificates

If you want to migrate the private keys and certificates from a different certificate application system to Certificates Manager, you must export a PFX or PKCS12 file from the system and import the file to Certificates Manager in the Key Management Service \(KMS\) console.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region of Certificates Manager.

3.  In the left-side navigation pane, click **Certificate**.

4.  Click **Import key and certificate**.

5.  In the Import key and certificate \(password protected PKCS12 format\) dialog box, set the **PKCS12 password** parameter. Then, upload your PKCS12 file or enter the content of the file.

6.  Click **OK**.

    **Note:** After private keys and certificates are imported, you can export them. If you want to increase the security level of a private key, you must set the **Exportable Key** parameter to **No** when you create the certificate. For more information, see [Create a certificate and download the CSR](/intl.en-US/Certificates Manager/Quick start.md).


