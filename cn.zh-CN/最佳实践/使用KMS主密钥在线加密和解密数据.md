# 使用KMS主密钥在线加密和解密数据

阿里云用户在云上部署IT资产，需要对敏感数据进行加密保护。如果被加密的数据对象较小（小于6KB），则可以通过密钥管理服务KMS（Key Management Service）的密码运算API，在线对数据直接加解密。

典型的使用场景包括（但不限于）：

-   对配置文件的加密
-   对SSL私钥的加密

本文以加密SSL证书私钥为例，介绍如何调用KMS API实现对数据的在线加密和解密。

## 产品架构

用户的数据会通过安全信道传递到KMS服务端，服务端完成加密和解密后，操作结果通过安全信道返回给用户。具体架构如下图所示。

![产品架构](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6968428951/p56539.png)

操作流程如下：

1.  通过[KMS控制台](https://kms.console.aliyun.com)或者调用CreateKey接口，创建一个用户主密钥（CMK）。
2.  调用KMS服务的Encrypt接口，将明文证书加密为密文证书。
3.  将密文证书部署在云服务器上。
4.  当服务器启动需要使用证书时，调用KMS服务的Decrypt接口将密文证书解密为明文证书。

## 相关API

您可以调用以下KMS API，完成对数据的加密或解密操作。

|API名称|说明|
|-----|--|
|[CreateKey](/cn.zh-CN/API参考/密钥/CreateKey.md)|创建用户主密钥（CMK）。|
|[CreateAlias](/cn.zh-CN/API参考/密钥/CreateAlias.md)|为指定用户主密钥创建一个别名。|
|[Encrypt](/cn.zh-CN/API参考/密钥/Encrypt.md)|指定CMK，由KMS加密数据。|
|[Decrypt](/cn.zh-CN/API参考/密钥/Decrypt.md)|解密KMS直接加密的数据，不需要指定CMK。|

## 加密/解密证书密钥

1.  调用CreateKey，创建用户主密钥。

    ```
    aliyun kms CreateKey
    ```

    预期输出：

    ```
    {
      "KeyMetadata": {
        "CreationDate": "2019-04-08T07:45:54Z",
        "Description": "",
        "KeyId": "1234abcd-12ab-34cd-56ef-12345678****",
        "KeyState": "Enabled",
        "KeyUsage": "ENCRYPT/DECRYPT",
        "DeleteDate": "",
        "Creator": "151266687691****",
        "Arn": "acs:kms:cn-hangzhou:151266687691****:key/1234abcd-12ab-34cd-56ef-12345678****",
        "Origin": "Aliyun_KMS",
        "MaterialExpireTime": ""
      },
      "RequestId": "2a37b168-9fa0-4d71-aba4-2077dd9e80df"
    }
    ```

2.  给主密钥添加别名（推荐步骤）。

    别名是用户主密钥的可选标识。如果用户不创建别名，也可以直接使用密钥的ID。

    ```
    aliyun kms CreateAlias --AliasName alias/Apollo/WorkKey --KeyId 1234abcd-12ab-34cd-56ef-12345678****
    ```

    **说明：** 其中，`Apollo/WorkKey`表示Apollo项目中的工作密钥（当前被用于加密的密钥），并在后续示例代码中使用此别名。即表示应用可以使用`alias/Apollo/WorkKey`调用加密API。

3.  加密证书私钥（业务系统对SSL私钥证书进行加密保护）。

    示例代码中：

    -   用户主密钥别名：`alias/Apollo/WorkKey`。
    -   明文证书文件：./certs/key.pem。
    -   输出的密文证书文件：./certs/key.pem.cipher。
    ```
    #!/usr/bin/env python
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

4.  解密证书私钥（业务系统对部署在云上的密文证书私钥进行解密）。

    示例代码中：

    -   部署的密文证书文件：./certs/key.pem.cipher。
    -   输出的明文证书文件：./certs/decrypted\_key.pem。
    ```
    #!/usr/bin/env python
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


