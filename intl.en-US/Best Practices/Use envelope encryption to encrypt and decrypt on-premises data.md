# Use envelope encryption to encrypt and decrypt on-premises data

You must encrypt sensitive information in your IT assets that are deployed on Alibaba Cloud. If you need to encrypt a large amounts of on-premises data, you can call cryptographic API operations of Key Management Service \(KMS\) to generate a data key online and then use the data key to encrypt the on-premises data offline. This encryption mechanism is known as envelope encryption.

You can use envelope encryption in, but not limited to, the following scenarios:

-   Encrypt business data files.
-   Encrypt all data stored on on-premises disks.

This topic shows you how to use envelope encryption to encrypt and decrypt on-premises files.

## How data encryption and decryption work

Use KMS to create a customer master key \(CMK\), use the CMK to generate a data key, and then use the data key to encrypt and decrypt on-premises files. Envelope encryption is suitable for encrypting large volumes of data. The following figure shows the envelope encryption procedure.

-   Envelope encryption

    ![encryption1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5668876951/p58526.png)

    Procedure:

    1.  Create a CMK in the KMS console or by calling the CreateKey operation.
    2.  Call the GenerateDataKey operation to generate a data key. KMS returns the plaintext and ciphertext of the data key.
    3.  Use the plaintext data key to encrypt the on-premises files and then delete the plaintext data key from the memory.
    4.  Store the ciphertext data key and encrypted data files on a persistent storage device or service.
-   Envelope decryption

    ![encry](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5668876951/p58527.png)

    Procedure:

    1.  Retrieve the ciphertext data key from the on-premises files.
    2.  Call the Decrypt operation of KMS to decrypt the ciphertext data key. The plaintext of the data key is returned.
    3.  Use the plaintext data key to decrypt the on-premises files and then delete the plaintext data key from the memory.

## Encryption and decryption API operations

You can call the KMS API operations described in the following table to encrypt and decrypt on-premises files.

|Operation|Description|
|---------|-----------|
|[CreateKey](/intl.en-US/API Reference/Key/CreateKey.md)|Creates a CMK.|
|[t22697.md\#](/intl.en-US/API Reference/Key/CreateAlias.md)|Assigns an alias to a CMK.|
|[GenerateDataKey](/intl.en-US/API Reference/Key/GenerateDataKey.md)|Generates a data key, uses a specified CMK to encrypt the data key, and then returns the plaintext and ciphertext of the data key.|
|[Decrypt](/intl.en-US/API Reference/Key/Decrypt.md)|Decrypts data that is encrypted in KMS, including the ciphertext data key generated by calling the GenerateDataKey operation. You do not need to specify a CMK.|

## Encrypt and decrypt on-premises files

You can create a CMK and encrypt and decrypt on-premises files by using Alibaba Cloud Command Line Interface \(CLI\).

1.  Create a CMK.

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

2.  Optional. Assign an alias to the CMK.

    Aliases, which are optional, are used to identify CMKs. If a CMK does not have an alias, you can use the ID of the CMK.

    ```
    $ aliyun kms CreateAlias --AliasName alias/Apollo/WorkKey --KeyId 1234abcd-12ab-34cd-56ef-12345678****
    ```

    **Note:** In this example, Apollo/WorkKey is assigned to the CMK in the Apollo project as the alias for key encryption. You can use the alias alias/Apollo/WorkKey in subsequent sample code to call the Encrypt API operation.

3.  Encrypt an on-premises file.

    In the following sample code:

    -   `alias/Apollo/WorkKey` is the alias of the CMK.
    -   ./data/sales.csv is the plaintext data file.
    -   ./data/sales.csv.cipher is the returned ciphertext data file.
    ```
    #! /usr/bin/env python
    #coding=utf-8
    
    import json
    import base64
    
    from Crypto.Cipher import AES
    
    from aliyunsdkcore import client
    from aliyunsdkkms.request.v20160120 import GenerateDataKeyRequest
    
    def KmsGenerateDataKey(client, key_alias):
        request = GenerateDataKeyRequest.GenerateDataKeyRequest()
        request.set_accept_format('JSON')
        request.set_KeyId(key_alias)
        request.set_NumberOfBytes(32)
        response = json.loads(client.do_action(request))
    
        datakey_encrypted = response["CiphertextBlob"]
        datakey_plaintext = response["Plaintext"]
        return (datakey_plaintext, datakey_encrypted)
    
    def ReadTextFile(in_file):
      file = open(in_file, 'r')
      content = file.read()
      file.close()
      return content
    
    def WriteTextFile(out_file, lines):
      file = open(out_file, 'w')
      for ln in lines:
        file.write(ln)
        file.write('\n')
      file.close()
    
    # Out file format (text)
    # Line 1: b64 encoded data key
    # Line 2: b64 encoded IV
    # Line 3: b64 encoded ciphertext
    # Line 4: b64 encoded authentication tag
    def LocalEncrypt(datakey_plaintext, datakey_encrypted, in_file, out_file):
      data_key_binary = base64.b64decode(datakey_plaintext)
      cipher = AES.new(data_key_binary, AES.MODE_EAX)
    
      in_content = ReadTextFile(in_file)
      ciphertext, tag = cipher.encrypt_and_digest(in_content)
    
      lines = [datakey_encrypted, base64.b64encode(cipher.nonce), base64.b64encode(ciphertext), base64.b64encode(tag)];
      WriteTextFile(out_file, lines)
    
    clt = client.AcsClient('Access-Key-Id','Access-Key-Secret','Region-Id')
    
    key_alias = 'alias/Apollo/WorkKey'
    
    in_file = './data/sales.csv'
    out_file = './data/sales.csv.cipher'
    
    # Generate Data Key
    datakey = KmsGenerateDataKey(clt, key_alias)
    
    # Locally Encrypt the sales record
    LocalEncrypt(datakey[0], datakey[1], in_file, out_file)
    ```

4.  Decrypt an on-premises file.

    In the following sample code:

    -   ./data/sales.csv.cipher is the ciphertext data file.
    -   ./data/decrypted\_sales.csv is the returned plaintext data file.
    ```
    #! /usr/bin/env python
    #coding=utf-8
    
    import json
    import base64
    
    from Crypto.Cipher import AES
    
    from aliyunsdkcore import client
    from aliyunsdkkms.request.v20160120 import DecryptRequest
    
    def KmsDecrypt(client, ciphertext):
      request = DecryptRequest.DecryptRequest()
      request.set_accept_format('JSON')
      request.set_CiphertextBlob(ciphertext)
      response = json.loads(client.do_action(request))
      return response.get("Plaintext")
    
    def ReadTextFile(in_file):
      file = open(in_file, 'r')
      lines = []
      for ln in file:
        lines.append(ln)
      file.close()
      return lines
    
    def WriteTextFile(out_file, content):
      file = open(out_file, 'w')
      file.write(content)
      file.close()
    
    def LocalDecrypt(datakey, iv, ciphertext, tag, out_file):
      cipher = AES.new(datakey, AES.MODE_EAX, iv)
      data = cipher.decrypt_and_verify(ciphertext, tag).decode('utf-8')
      WriteTextFile(out_file, data)
    
    clt = client.AcsClient('Access-Key-Id','Access-Key-Secret','Region-Id')
    
    in_file = './data/sales.csv.cipher'
    out_file = './data/decrypted_sales.csv'
    
    # Read encrypted file
    in_lines = ReadTextFile(in_file)
    
    # Decrypt data key
    datakey = KmsDecrypt(clt, in_lines[0])
    
    # Locally decrypt the sales record
    LocalDecrypt(
      base64.b64decode(datakey),
      base64.b64decode(in_lines[1]), # IV
      base64.b64decode(in_lines[2]), # Ciphertext
      base64.b64decode(in_lines[3]), # Authentication tag
      out_file
      )
    ```

