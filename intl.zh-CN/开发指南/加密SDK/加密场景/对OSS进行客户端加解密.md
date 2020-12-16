# 对OSS进行客户端加解密

当您对对象存储OSS进行客户端加解密时，每个对象（Object）将使用一个数据密钥。本文为您介绍如何对OSS对象进行客户端加解密。

## 使用场景

当使用KMS托管用户主密钥用于客户端数据加密时，无需向加密客户端提供任何加密密钥，只需在上传对象时指定KMS用户主密钥资源名称（CMK ARN）即可。

## 加密机制

![OSS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0769086061/p186891.png)

1.  获取加密密钥。

    通过使用CMK ARN，加密SDK（Encryption SDK）首先向KMS发送一个请求，申请一个用于加密Object的数据密钥（Data Key）。作为响应，KMS会返回一个随机生成的数据密钥明文（Data Key）以及一个数据密钥密文（Encrypted Data Key）。

2.  加密数据并上传至OSS。

    加密SDK接收到KMS返回的数据密钥明文以及数据密钥密文后，将使用数据密钥明文进行本地加密，然后将数据密钥密文封装到消息头并存储到对象元数据，最后将加密的对象上传到OSS。


## 解密机制

1.  下载Object。

    加密SDK从OSS服务端下载加密的Object以及作为对象元数据存储的消息头，并解析消息头得到数据密钥密文。

2.  解密Object。

    加密SDK从CMK ARN中解析出地域信息，将数据密钥密文发送至对应地域的KMS服务器。作为响应，KMS将使用指定的CMK对数据密钥密文进行解密，并且将数据密钥明文返回给本地加密客户端。加密SDK使用数据密钥明文对加密后的对象进行解密，得到原始对象。


**说明：** 使用GCM（Galois Counter Mode）模式对数据对象进行加密，解密时可以对数据进行整体解密，也可以对指定的分段数据进行解密。整体解密时会验证数据的完整性校验数据，校验通过后得到解密数据，分段解密时不对数据完整性进行校验，只对分段数据进行解密。

## 代码示例

您可以通过[OSSEncryption](https://github.com/aliyun/alibabacloud-encryption-sdk-java/blob/master/src/examples/java/com/aliyun/encryptionsdk/examples/oss/OSSEncryptionSample.java)获取SDK代码示例。

