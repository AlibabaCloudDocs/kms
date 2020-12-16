# Generate and verify digital signatures

You can use the private key of an asymmetric customer master key \(CMK\) to sign messages or other information. Private keys are strictly protected. Only a trusted user can use a private key to sign data. The public key that matches the private key can be used to verify the generated signature.

The signature generation and verification feature provides the following benefits:

-   Verifies data integrity. If the data does not match its signature, the data may have been tampered with.
-   Verifies message authenticity. If a message does not match its signature, the message transmitter does not hold the private key.
-   Provides non-repudiation for signatures. If the data matches its signature, the signer cannot deny this signature.

## Sample code

```
/**
 *
 * Sample code for signature generation and verification
 */
public class DigestMessageSignatureVerifySample {
    private static final String ASYM_CMK_ARN = "acs:kms:RegionId:UserId:key/CmkId";
    private static final String KEY_VERSION_ID = "<KEY_VERSION_ID>";
    // accessKeyId accessKeySecret
    private static final String ACCESS_KEY_ID = "<AccessKeyId>";
    private static final String ACCESS_KEY_SECRET = "<AccessKeySecret>";
    private static final byte[] MESSAGE_TEXT = "this is test.".getBytes();
    private static final byte[] DIGEST_HEX_TEXT = "FECC75FE2A23D8EAFBA452EE0B8B6B56BECCF52278BF1398AADDEECFE0EA0FCE".getBytes();

    public static void main(String[] args) {
        // Configure Alibaba Cloud access parameters.
        AliyunConfig config = new AliyunConfig();
        config.withAccessKey(ACCESS_KEY_ID, ACCESS_KEY_SECRET);

        // Create an SDK and pass in the Alibaba Cloud access parameters.
        AliyunCrypto aliyunCrypto = new AliyunCrypto(config);
        
        // Configure a provider for signature generation and verification.
        SignatureProvider provider = new KmsAsymmetricKeyProvider(ASYM_CMK_ARN, KEY_VERSION_ID, SignatureAlgorithm.RSA_PKCS1_SHA_256);

        // Use the original message.
        byte[] signature = aliyunCrypto.sign(provider, MESSAGE_TEXT, ContentType.MESSAGE).getResult();
        Boolean isOk = aliyunCrypto.verify(provider, MESSAGE_TEXT, signature, ContentType.MESSAGE).getResult();
        assertTrue(isOk);

        // Use the message digest.
        byte[] sha256Digest = hex2Bytes(DIGEST_HEX_TEXT);
        signature = aliyunCrypto.sign(provider, sha256Digest, ContentType.DIGEST).getResult();
        isOk = aliyunCrypto.verify(provider, sha256Digest, signature, ContentType.DIGEST).getResult();
        assertTrue(isOk);
    }
}
```

**Note:** For the complete sample code, see [libabacloud-encryption-sdk-java-examples-signVerify](https://github.com/aliyun/alibabacloud-encryption-sdk-java/tree/master/src/examples/java/com/aliyun/encryptionsdk/examples/signVerify).

