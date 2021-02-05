# Encrypt sensitive data in a database

Data encryption in a database is a proactive measure of data protection. It prevents data leaks that are caused by plaintext storage and data theft that is performed by privileged users. It also helps defend against hackers that break through the security boundary. This way, the issue of sensitive data leaks can be fundamentally resolved. This topic describes the scenarios of sensitive data encryption in a database and how to encrypt and decrypt data. This topic also provides an example of encrypting sensitive data in a database.

## Scenarios

-   Prevent sensitive data leaks caused by plaintext storage after a data breach.

    In most cases, data in a database is stored and used in plaintext. If data files or backup files are disclosed, serious data leaks may occur. In data breach attacks, data stored in plaintext has no secrets for attackers. To resolve this issue, you must encrypt your data to prevent data leaks.

-   Prevent data leaks caused by data theft that is performed by privileged users.

    Database encryption is independent of the permission control system of a database. Database encryption can help enhance permission control. You can use a dedicated encryption system to configure access permissions on sensitive data. This effectively controls the access to sensitive data from privileged users such as database superusers and ensures data security.


## How to encrypt and decrypt data

-   Encryption
    1.  Create a data key.

        Encryption SDK calls the GenerateDataKey operation to request a data key from Key Management Service \(KMS\). KMS returns the data key and its ciphertext.

    2.  Encrypt and store data.
        1.  Use the data key to encrypt data and encode the ciphertext data by using the Base64 algorithm.
        2.  Store the Base64-encoded ciphertext data in a database.
-   Decryption

    Query and decrypt data.

    1.  Read ciphertext data from the database.
    2.  Decode the ciphertext data by using the Base64 algorithm. Encryption SDK calls the decrypt method to decrypt the ciphertext data key. KMS returns the decrypted data key to Encryption SDK.
    3.  Decrypt data. Encryption SDK uses the data key to decrypt the ciphertext data and obtain the plaintext data.

## Example

Encryption SDK encrypts data to be transmitted from applications to databases. KMS generates and manages the encryption keys.

The following code provides an example on how to encrypt and decrypt the name field in the User table. In this example, each field uses a data key. Data keys are cached during decryption. When you query the same field for multiple times, you can use the data key that is cached.

To ensure that a field can store encrypted data, you must increase the size of the field. Increase the size of a field to three times that of the original size.

-   Define an entity class.

    ```
    @Entity
    public class User {
        @Id
        @GeneratedValue
        private Long id;
    
        private String name;
        private String email;
    
        public Long getId() {
            return id;
        }
        public void setId(Long id) {
            this.id = id;
        }
        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
        public String getEmail() {
            return email;
        }
        public void setEmail(String email) {
            this.email = email;
        }
    }
    ```

-   Define the UserRepository class.

    ```
    public interface UserRepository extends CrudRepository<User, Long> {
    }
    ```

-   Implement the JPA AttributeConverter interface.

    The EncryptionConverter class calls the methods of Encryption SDK to obtain a data key to encrypt and decrypt the specified data.

    ```
    @Converter
    public class EncryptionConverter implements AttributeConverter<String, String> {
        private static String ACCESS_KEY_ID = "<AccessKeyId>";
        private static String ACCESS_KEY_SECRET = "<AccessKeySecret>";
        private static String CMK_ARN = "acs:kms:RegionId:UserId:key/CmkId";
        private static AliyunConfig config;
        static {
            config = new AliyunConfig();
            config.withAccessKey(ACCESS_KEY_ID, ACCESS_KEY_SECRET);
        }
    
        @Override
        public String convertToDatabaseColumn(String plainText) {
            BaseDataKeyProvider dataKeyProvider = new DefaultDataKeyProvider(CMK_ARN);
            AliyunCrypto crypto = new AliyunCrypto(config);
    
            try {
                CryptoResult<byte[]> encryptResult = crypto.encrypt(dataKeyProvider, plainText.getBytes(StandardCharsets.UTF_8), Collections.singletonMap("sample", "context"));
                return Base64.getEncoder().encodeToString(encryptResult.getResult());
            } catch (InvalidAlgorithmException e) {
                System.out.println("Failed.") ;
                System.out.println("Error message: " + e.getMessage());
            }
            return null;
        }
    
        @Override
        public String convertToEntityAttribute(String cipherText) {
            BaseDataKeyProvider dataKeyProvider = new DefaultDataKeyProvider(CMK_ARN);
            AliyunCrypto crypto = new AliyunCrypto(config);
            // *** Cache a customer master key (CMK) ***
            CryptoKeyManager ckm = new CachingCryptoKeyManager(new LocalDataKeyMaterialCache())
            crypto.setCryptoKeyManager(ckm);
            try {
                CryptoResult<byte[]> decryptResult = crypto.decrypt(dataKeyProvider, Base64.getDecoder().decode(cipherText));
                return new String(decryptResult.getResult(), StandardCharsets.UTF_8);
            } catch (InvalidAlgorithmException | UnFoundDataKeyException e) {
                e.printStackTrace();
            }
            return null;
        }
    }
    ```

-   Add the @Convert annotation.

    Add the @Convert annotation to the attribute that needs to be encrypted. The attribute is a column in the database.

    ```
        @Convert(converter = EncryptionConverter.class)
        private String name;
    ```


For more information about the examples of sensitive data encryption in databases, visit [alibabacloud-encryption-sdk-java](https://github.com/aliyun/alibabacloud-encryption-sdk-java/tree/master/src/examples/java/com/aliyun/encryptionsdk/examples/jpaencryption).

