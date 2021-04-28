# Quick start

You can use Certificates Manager to manage keys and certificates and generate or verify signatures. This topic describes how to create a certificate, download the certificate signing request \(CSR\), import a certificate, and use a certificate.

## Step 1: Create a certificate and download the CSR

1.  Log on to the [Key Management Service \(KMS\) console](https://kms.console.aliyun.com).

2.  In the upper-left corner of the page, select the region in which you want to create a certificate.

3.  In the left-side navigation pane, click **Certificate**.

4.  On the page that appears, click **Create Certificate**.

5.  In the Create Certificate dialog box, set the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**CommonName\(CN\)**|The name of the certificate subject.|
    |**Country\(C\)**|The two-character country or region code in the [ISO 3166-1](https://www.iso.org/obp/ui/#search/code/) standard. For example, CN indicates China.|
    |**StateOrProvince\(ST\)**|The name of the province, municipality, autonomous region, or special administrative region.|
    |**Locality\(L\)**|The name of the city.|
    |**Organization\(O\)**|The legal name of the enterprise, company, organization, or institution. You can click the plus sign \(+\) to add more organization names. |
    |**OrganizationUnit\(OU\)**|The name of the department. You can click the plus sign \(+\) to add more department names. |
    |**Email\(E\)**|The email address of the certificate holder or administrator.|
    |**SubjectAlternativeNames**|If the certificate is a domain validated \(DV\) certificate, you can add subject alternative names to generate a multi-domain CSR. Click the plus sign \(+\), enter a subject alternative name, and then click the ![right](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1554759161/p269037.png) icon. |
    |**Key Spec**|The type of the key. Valid values:    -   RSA\_2048
    -   EC\_SM2
    -   EC\_P256
**Note:** Select an option based on the algorithm supported by the certificate application system. EC\_P256 provides higher security whereas RSA\_2048 provides better compatibility. However, some application systems will stop supporting RSA\_2048 keys on December 31, 2030. |
    |**Exportable Key**|Specifies whether the private key of the certificate can be exported for use. Valid values:    -   Yes: The private key of the certificate can be exported for use.
    -   No: The private key of the certificate cannot be exported for use. We recommend that you select No to protect keys with a higher security level. |

6.  Click **Create Certificate**.

7.  In the **Successfully created certificate** dialog box, click **Download certificate request**.

8.  Click **OK**.


## Step 2: Obtain the certificate issued by a CA

Submit the CSR file that you downloaded in [Step 1](#section_ts0_7x8_93y) to a certificate authority \(CA\) to obtain the formal certificate and certificate chain.

## Step 3: Import the certificate

1.  In the certificate list, find the certificate and choose **More** \> **Import certificate** in the **Operating** column.

2.  In the Import certificate dialog box, upload the certificate and certificate chain that you obtained in [Step 2](#section_ohx_1tf_7ca) or enter their content.

3.  Click **OK**.

    After the certificate is imported, the certificate enters the **Active** state. You can use the certificate to perform operations as required. For example, you can use it to manage keys and generate or verify signatures.


## Step 4: Use the certificate to generate a signature

-   Method 1: Call the [CertificatePrivateKeySign](/intl.en-US/API Reference/Certificate/CertificatePrivateKeySign.md) operation to generate a digital signature by using the certificate.
-   Method 2: Use KMS SDK to generate a digital signature by using the certificate. For more information, see [SDK overview](/intl.en-US/Developer Guide/KMS SDK/SDK overview.md). Sample code in Java:

    ```
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.kms.model.v20160120.CertificatePrivateKeySignRequest;
    import com.aliyuncs.kms.model.v20160120.CertificatePrivateKeySignResponse;
    import org.apache.commons.codec.binary.Base64;
    
    /**
     *  @param client Alibaba Cloud SDK Client. For more information, see the documentation of Alibaba Cloud SDK for Java. 
     *  @param certId The ID of the certificate to be used. 
     *  @param sigAlg The digital signature algorithm. For more information, see the reference document for the KMS API operation CertificatePrivateKeySign. 
     *  @param message The content to be signed, which must be less than or equal to 4 KB. 
     */
    public byte[] doSignByCertificate(DefaultAcsClient client, String certId, String sigAlg, byte[] message) throws ClientException {
        String msgB64 = Base64.encodeBase64String(message); // Encode the content to be signed in Base64. 
        CertificatePrivateKeySignRequest request = new CertificatePrivateKeySignRequest();
        request.setCertificateId(certId);
        request.setAlgorithm(sigAlg);
        request.setMessage(msgB64);
    
        CertificatePrivateKeySignResponse response = client.getAcsResponse(request);
    
        String sigB64 = response.getSignatureValue();
        return Base64.decodeBase64(sigB64); // Decode the returned data in Base64 to obtain the signature value. 
    }
    ```


## Step 5: Use the certificate to verify a signature

-   Method 1: Call the [CertificatePublicKeyVerify](/intl.en-US/API Reference/Certificate/CertificatePublicKeyVerify.md) operation to verify a digital signature by using the certificate.
-   Method 2: Use KMS SDK to verify a digital signature by using the certificate. For more information, see [SDK overview](/intl.en-US/Developer Guide/KMS SDK/SDK overview.md). Sample code in Java:

    ```
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.kms.model.v20160120.CertificatePublicKeyVerifyRequest;
    import com.aliyuncs.kms.model.v20160120.CertificatePublicKeyVerifyResponse;
    import org.apache.commons.codec.binary.Base64;
    
    /**
     *  @param client Alibaba Cloud SDK Client. For more information, see the documentation of Alibaba Cloud SDK for Java. 
     *  @param certId The ID of the certificate to be used. 
     *  @param sigAlg The digital signature algorithm. For more information, see the reference document for the KMS API operation CertificatePrivateKeySign. 
     *  @param message The content to be verified, which must be less than or equal to 4 KB. 
     *  @param signature The digital signature of the content to be verified. 
     */
    public Boolean doVerifyByCertificate(DefaultAcsClient client, String certId, String sigAlg, byte[] message, byte[] signature) throws ClientException {
        String msgB64 = Base64.encodeBase64String(message); // Encode the content to be verified in Base64. 
        String sigB64 = Base64.encodeBase64String(signature); // Encode the signature value in Base64. 
        CertificatePublicKeyVerifyRequest request = new CertificatePublicKeyVerifyRequest();
        request.setCertificateId(certId);
        request.setAlgorithm(sigAlg);
        request.setMessage(msgB64);
        request.setSignatureValue(sigB64);
    
        CertificatePublicKeyVerifyResponse response = client.getAcsResponse(request);
    
        return response.getSignatureValid();
    }
    ```


