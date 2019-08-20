# 使用KMS信封加密在本地加密、解密数据 {#concept_221281 .concept}

阿里云用户在云上部署IT资产，需要对敏感数据进行加密保护。如果被加密的数据对象较大，则可以通过KMS的密码运算API在线生成数据密钥，用离线数据密钥在本地加密大量数据。这类加密模式叫作信封加密。

## 场景概述 {#section_r5y_ka6_fsp .section}

典型的场景包括（但不限于）：

-   对业务数据文件的加密
-   对全磁盘数据加密

本文以加密本地文件为例，介绍如何使用KMS实现对数据的信封加密，以及如何解密被信封加密的数据。

## 产品架构 {#section_a1n_02b_nck .section}

使用KMS创建一个主密钥，使用主密钥生成一个数据密钥，再使用数据密钥在本地加解密数据。这种场景适用于大量数据的加解密。具体架构如下所示。

-   [信封加密](#li_7t1_wkl_j1k)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1422781/156628479956487_zh-CN.jpg)

    操作流程如下：

    1.  通过[KMS控制台](https://kms.console.aliyun.com/?spm=a2c4g.11186623.2.21.aa46717dmqOatF)，或者调用CreateKey接口，创建一个用户主密钥。
    2.  调用KMS服务的GenerateDataKey接口创建一个数据密钥。KMS会返回一个明文的数据密钥和一个密文的数据密钥。
    3.  使用明文的数据密钥加密文件，产生密文文件，然后销毁内存中的明文密钥。
    4.  用户将密文数据密钥和密文文件一同存储到持久化存储设备或服务中。
-   [信封解密](#li_jr5_gbw_ni2)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1422781/156628479956499_zh-CN.png)

    操作流程如下：

    1.  从本地文件中读取密文数据密钥。
    2.  调用KMS服务的Decrypt接口，将加密过的密钥解密为明文密钥。
    3.  用明文密钥为本地数据解密，再销毁内存中的明文密钥。

## 相关API {#section_249_y34_gvm .section}

您可以调用以下KMS API，在本地对数据进行加解密。

|API名称|说明|
|-----|--|
|[CreateKey](https://help.aliyun.com/document_detail/28947.html)|创建用户主密钥（CMK）。|
|[CreateAlias](https://help.aliyun.com/document_detail/68624.html)|为指定用户主密钥创建一个别名。|
|[GenerateDataKey](https://help.aliyun.com/document_detail/28948.html)|在线生成数据密钥，用指定CMK加密数据密钥后，返回数据密钥的密文和明文。|
|[Decrypt](https://help.aliyun.com/document_detail/28950.html)|解密KMS直接加密的数据（包括GenerateDataKey产生的数据密钥的密文），不需要指定CMK。|

## 加密/解密本地文件 {#section_ydw_24q_sqa .section}

-   信封加密
    1.  创建用户主密钥

        ``` {#codeblock_37x_bv0_5em}
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

    2.  给主密钥添加别名（可选）

        别名是用户主密钥的可选标识。如果用户不创建别名，也可以直接使用密钥的ID。

        ``` {#codeblock_ash_cgr_mnt}
        $ aliyun kms CreateAlias --AliasName alias/Apollo/WorkKey --KeyId 1234abcd-12ab-34cd-56ef-1234567890ab
        ```

        **说明：** 其中，Apollo/WorkKey表示Apollo项目中的工作密钥（当前被用于加密的密钥），并在后续示例代码中使用此别名。即表示应用可以使用alias/Apollo/WorkKey调用加密API。

    3.  加密本地文件

        示例代码中：

        -   用户主密钥：别名为`alias/Apollo/WorkKey`
        -   明文数据文件：./data/sales.csv
        -   输出的密文数据文件：./data/sales.csv.cipher
        ``` {#codeblock_f6g_z14_ro9}
        #!/usr/bin/env python
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

-   信封解密

    解密本地文件

    示例代码中：

    -   密文数据文件：./data/sales.csv.cipher
    -   输出的明文数据文件：./data/decrypted\_sales.csv
    ``` {#codeblock_2hq_0j2_hxt}
    #!/usr/bin/env python
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
      response = json.loads(clt.do_action(request))
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


