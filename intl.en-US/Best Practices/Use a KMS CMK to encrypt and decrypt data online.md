# Use a KMS CMK to encrypt and decrypt data online

You must encrypt sensitive information in your IT assets that are deployed on Alibaba Cloud. You can call cryptographic API operations of Key Management Service \(KMS\) to encrypt or decrypt data less than 6 KB online.

You can use this feature in, but not limited to, the following typical scenarios:

-   Encrypt configuration files.
-   Encrypt private keys of Secure Sockets Layer \(SSL\) certificates.

This topic shows you how to call KMS API operations to encrypt and decrypt private keys of SSL certificates online.

## Architecture

User data is transmitted to the KMS server over an encrypted channel. The KMS server encrypts or decrypts the data and then returns the data to the user over the encrypted channel. The following figure shows the architecture.

![encryption](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4221892951/p58524.png)

Procedure:

1.  Create a customer master key \(CMK\) in the [KMS console](https://kms.console.aliyun.com) or by calling the CreateKey operation.
2.  Call the Encrypt operation of KMS to encrypt the private key of an SSL certificate. The ciphertext of the private key is returned.
3.  Install the SSL certificate and the encrypted private key on an Elastic Compute Service \(ECS\) instance.
4.  Call the Decrypt operation of KMS to decrypt the encrypted private key when the ECS instance starts and needs to use the SSL certificate.

## Related API operations

You can call the following KMS API operations to encrypt and decrypt data.

|Operation|Description|
|---------|-----------|
|[CreateKey](/intl.en-US/API Reference/Key/CreateKey.md)|Creates a CMK.|
|[t22697.md\#](/intl.en-US/API Reference/Key/CreateAlias.md)|Assigns an alias to a CMK.|
|[Encrypt](/intl.en-US/API Reference/Key/Encrypt.md)|Encrypts data by using a specified CMK.|
|[Decrypt](/intl.en-US/API Reference/Key/Decrypt.md)|Decrypts data that is encrypted by KMS. You do not need to specify a CMK.|

## Encrypt and decrypt the private key of an SSL certificate

1.  Call the CreateKey operation to create a CMK.

    ```
    $ aliyun kms CreateKey
    {
      "KeyMetadata": {
        "CreationDate": "2019-04-08T07:45:54Z",
        "Description": "",
        "KeyId": "1234abcd-12ab-34cd-56ef-12345678****",
        "KeyState": "Enabled",
        "KeyUsage": "ENCRYPT/DECRYPT",
        "DeleteDate": "",
        "Creator": "111122223333",
        "Arn": "acs:kms:cn-hangzhou:111122223333:key/1234abcd-12ab-34cd-56ef-12345678****",
        "Origin": "Aliyun_KMS",
        "MaterialExpireTime": ""
      },
      "RequestId": "2a37b168-9fa0-4d71-aba4-2077dd9e80df"
    }
    ```

2.  Assign an alias to the CMK. We recommend that you perform this step.

    Aliases are optional to CMKs. If a CMK does not have an alias, you can use the ID of the CMK.

    ```
    $ aliyun kms CreateAlias --AliasName alias/Apollo/WorkKey --KeyId 1234abcd-12ab-34cd-56ef-12345678****
    ```

    **Note:** In this example, `Apollo/WorkKey` is assigned to the CMK used in the Apollo project as the alias. This alias is used in the subsequent sample code. You can use `alias/Apollo/WorkKey` to reference the CMK when you call the Encrypt operation.

3.  Encrypt the private key to protect it in your business system.

    In the following sample code:

    -   `alias/Apollo/WorkKey` is the alias of the CMK.
    -   ./certs/key.pem is the plaintext key file.
    -   ./certs/key.pem.cipher is the ciphertext key file.
    ```
    #! /usr/bin/env python
    #coding=utf-8
    
    import json
    
    from aliyunsdkcore import client
    from aliyunsdkkms.request.v20160120 import EncryptRequest
    from aliyunsdkkms.request.v20160120 import DecryptRequest
    
    def KmsEncrypt(client, plaintext, key_alias):
      request = EncryptRequest.EncryptRequest()
      request.set_accept_format('JSON')
      request.set_KeyId(key_alias)
      request.set_Plaintext(plaintext)
      response = json.loads(client.do_action(request))
      return response.get("CiphertextBlob")
    
    def ReadTextFile(in_file):
      file = open(in_file, 'r')
      content = file.read()
      file.close()
      return content
    
    def WriteTextFile(out_file, content):
      file = open(out_file, 'w')
      file.write(content)
      file.close()
    
    clt = client.AcsClient('<Access-Key-Id>','Access-Key-Secret','<Region-Id>')
    
    key_alias = 'alias/Apollo/WorkKey'
    
    in_file = './certs/key.pem'
    out_file = './certs/key.pem.cipher'
    
    # Read private key file in text mode
    in_content = ReadTextFile(in_file)
    
    # Encrypt
    ciphertext = KmsEncrypt(clt, in_content, key_alias)
    
    # Write encrypted key file in text mode
    WriteTextFile(out_file, ciphertext)
    ```

4.  Decrypt the encrypted private key that you have installed on the ECS instance.

    In the following sample code:

    -   ./certs/key.pem.cipher is the ciphertext key file.
    -   ./certs/decrypted\_key.pem is the plaintext key file.
    ```
    #! /usr/bin/env python
    #coding=utf-8
    
    import json
    
    from aliyunsdkcore import client
    from aliyunsdkkms.request.v20160120 import EncryptRequest
    from aliyunsdkkms.request.v20160120 import DecryptRequest
    
    def KmsDecrypt(client, ciphertext):
      request = DecryptRequest.DecryptRequest()
      request.set_accept_format('JSON')
      request.set_CiphertextBlob(ciphertext)
      response = json.loads(client.do_action(request))
      return response.get("Plaintext")
    
    def ReadTextFile(in_file):
      file = open(in_file, 'r')
      content = file.read()
      file.close()
      return content
    
    def WriteTextFile(out_file, content):
      file = open(out_file, 'w')
      file.write(content)
      file.close()
    
    clt = client.AcsClient('<Access-Key-Id>','Access-Key-Secret','<Region-Id>')
    
    in_file = './certs/key.pem.cipher'
    out_file = './certs/decrypted_key.pem'
    
    # Read encrypted key file in text mode
    in_content = ReadTextFile(in_file)
    
    # Decrypt
    ciphertext = KmsDecrypt(clt, in_content)
    
    # Write Decrypted key file in text mode
    WriteTextFile(out_file, ciphertext)
    ```


