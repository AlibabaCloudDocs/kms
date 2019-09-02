# Use CMK encryption to encrypt and decrypt data online {#concept_221280 .concept}

You must encrypt sensitive information in your IT assets that are deployed on Alibaba Cloud. You can call cryptographic operations of Key Management Service \(KMS\) to encrypt or decrypt data less than 6 KB online.

## Scenarios {#section_juu_hzi_mmc .section}

You can use CMK encryption in many scenarios, including but not limited to the following:

-   Encrypt configuration files.
-   Encrypt private keys of SSL certificates.

This topic describes how to call the KMS API to encrypt and decrypt private keys of SSL certificates online.

## How CMK encryption works {#section_lpf_ze9_kkk .section}

User data is transmitted to the KMS server through an encrypted connection. The KMS server encrypts or decrypts the data, and then returns the data to the user through the encrypted connection. The following figure shows the entire procedure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1423112/156741282458524_en-US.png)

Procedure:

1.  Use the [KMS console](https://kms.console.aliyun.com/?spm=a2c4g.11186623.2.21.aa46717dmqOatF) or call the CreateKey operation to create a customer master key \(CMK\). For more information, see [Create a CMK](#li_fuk_c6c_zer).
2.  Call the Encrypt operation of KMS to encrypt the private key of an SSL certificate. A ciphertext copy of the private key is returned. For more information, see [Encrypt a private key](#li_rtd_wae_rgf).
3.  Install the SSL certificate and ciphertext private key on your cloud server.
4.  When the cloud server needs to create an encrypted connection, it calls the Decrypt operation of KMS to decrypt the ciphertext private key. For more information, see [Decrypt a private key](#li_c45_sur_ul0).

## Related API operations {#section_69c_ut2_ti8 .section}

You can call the following API operations to encrypt and decrypt data.

|Operation|Description|
|---------|-----------|
|[CreateKey](../../../../reseller.en-US/API Reference/API list/CreateKey.md#)|Creates a CMK.|
|[CreateAlias](../../../../reseller.en-US/API Reference/API list/CreateAlias.md#)|Assigns an alias to a CMK.|
|[Encrypt](../../../../reseller.en-US/API Reference/API list/Encrypt.md#)|Encrypts data with a specified CMK.|
|[Decrypt](../../../../reseller.en-US/API Reference/API list/Decrypt.md#)|Decrypts data that is encrypted by KMS. You do not need to specify a CMK.|

## Encrypt and decrypt the private key of an SSL certificate {#section_2b8_ixl_dd3 .section}

1.  Call the CreateKey operation to create a CMK.

    ``` {#codeblock_x09_4bl_9kx}
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

2.  Assign an alias to the CMK.

    Aliases are optional to CMKs. If a CMK does not have an alias, you can use its ID.

    ``` {#codeblock_eey_ei2_05k}
    $ aliyun kms CreateAlias --AliasName alias/Apollo/WorkKey --KeyId 1234abcd-12ab-34cd-56ef-12345678****
    ```

    **Note:** In this example, `Apollo/WorkKey` specifies the CMK in the Apollo project that is used to encrypt the private key. The alias of the CMK is WorkKey. This means that you can specify `alias/Apollo/WorkKey` to use the CMK WorkKey to encrypt a private key.

3.  Call the Encrypt operation to encrypt the private key. KMS then encrypts the private key.

    Sample code:

    -   CMK: The alias of the CMK is `alias/Apollo/WorkKey`.
    -   Plaintext private key: ./certs/key.pem
    -   Ciphertext private key: ./certs/key.pem.cipher
    ``` {#codeblock_yj0_rr5_f33}
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
      response = json.loads(clt.do_action(request))
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

4.  Call the Decrypt operation to decrypt the ciphertext private key. KMS then decrypts the private key that you have installed on your cloud server.

    Sample code:

    -   Ciphertext private key: ./certs/key.pem.cipher
    -   Plaintext private key: ./certs/decrypted\_key.pem
    ``` {#codeblock_lim_git_96t}
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
      response = json.loads(clt.do_action(request))
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


