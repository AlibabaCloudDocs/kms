# Import keys and certificates

To migrate keys and certificates from a certificate application system to Certificates Manager, you must export the key and certificate files from the system in the PFX or PKCS12 format. Then, you can import the key and certificate files into Certificates Manager in the Key Management Service \(KMS\) console.

1.  Log on to the [KMS console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region in which you want to create a certificate.

3.  In the left-side navigation pane, click **Certificate**. On the page that appears, click Import key and certificate.

4.  In the Import key and certificate \(password protected PKCS12 format\) dialog box, set the **PKCS12 password** parameter, and upload a PKCS12 file or enter the content of the file.

5.  Click **OK**.

    **Note:** You can export the imported keys and certificates. If you want to protect keys with a higher security level, you can set the **Exportable Key** parameter to **No** when you create a certificate. For more information, see [Create a certificate and download the CSR](/intl.en-US/Certificates Manager/Quick start.md).


