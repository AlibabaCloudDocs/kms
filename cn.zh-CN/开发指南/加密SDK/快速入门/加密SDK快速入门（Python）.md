# 加密SDK快速入门（Python）

加密SDK（Encryption SDK）是一个客户端密码库，通过与密钥管理服务KMS（Key Management Service）结合使用，帮助您快速实现数据的加解密、签名验签功能。本文以Python语言为例，为您介绍如何快速使用加密SDK进行数据加解密。

您可以访问[alibabacloud-encryption-sdk-python](https://github.com/aliyun/alibabacloud-encryption-sdk-python)，查看代码示例。

## 在本地安装加密SDK

1.  安装加密SDK。

    ```
    git clone https://github.com/aliyun/alibabacloud-encryption-sdk-python.git
    cd alibabacloud-encryption-sdk-python
    python setup.py install
    ```

2.  验证加密SDK版本。

    1.  执行以下命令，进入Python语言环境。

        ```
        python
        ```

    2.  执行以下命令，验证加密SDK版本。

        ```
        import aliyun_encryption_sdk
        aliyun_encryption_sdk.__version__
        ```

        执行命令后，Python控制台显示版本号`'0.1.1'`。


## 对字节数组类型的数据进行加解密

```
# -*- coding: UTF-8 -*-
"""Example showing basic encryption and decryption."""

import base64
import os

from aliyun_encryption_sdk.cache.local import LocalDataKeyMaterialCache
from aliyun_encryption_sdk.ckm.cache import CachingCryptoKeyManager
from aliyun_encryption_sdk.client import AliyunCrypto
from aliyun_encryption_sdk.kms import AliyunConfig
from aliyun_encryption_sdk.provider.default import DefaultDataKeyProvider


def build_aliyun_crypto(cache=False):
    config = AliyunConfig(ACCESS_KEY_ID, ACCESS_KEY_SECRET)
    client = AliyunCrypto(config)
    if cache:
        client.crypto_key_manager = CachingCryptoKeyManager(LocalDataKeyMaterialCache(), 5)
    return client


def encrypt_sample():
    print("原文: " + PLAIN_TEXT)
    provider = DefaultDataKeyProvider(AES_KEY_ARN)
    client = build_aliyun_crypto(False)
    cipher_text, enc_material = client.encrypt(provider, PLAIN_TEXT.encode("utf-8"), ENCRYPTION_CONTEXT)
    cipher_text_str = base64.standard_b64encode(cipher_text).decode("utf-8")
    print(u"加密密文: " + cipher_text_str)
    return cipher_text_str


def decrypt_sample(cipher_text):
    cipher_text_bytes = base64.standard_b64decode(cipher_text.encode("utf-8"))
    provider = DefaultDataKeyProvider(AES_KEY_ARN)
    client = build_aliyun_crypto(False)
    plain_text, dec_material = client.decrypt(provider, cipher_text_bytes)
    print(u"解密结果: " + bytes.decode(plain_text))
    return plain_text


if __name__ == '__main__':
    PLAIN_TEXT = "some plaintext"
    ACCESS_KEY_ID = os.getenv("ACCESS_KEY_ID")
    ACCESS_KEY_SECRET = os.getenv("ACCESS_KEY_SECRET")
    AES_KEY_ARN = os.getenv("AES_KEY_ARN")
    ENCRYPTION_CONTEXT = {
        "this": "context",
        "can help you": "to confirm",
        "this data": "is your original data"
    }
    cipherText = encrypt_sample()
    decrypt_sample(cipherText)
```

## 对字节流类型的数据进行加解密

```
# -*- coding: UTF-8 -*-
"""Example showing basic encryption and decryption."""

import os

from aliyun_encryption_sdk.cache.local import LocalDataKeyMaterialCache
from aliyun_encryption_sdk.ckm.cache import CachingCryptoKeyManager
from aliyun_encryption_sdk.client import AliyunCrypto
from aliyun_encryption_sdk.kms import AliyunConfig
from aliyun_encryption_sdk.provider.default import DefaultDataKeyProvider


def build_aliyun_crypto(cache=False):
    config = AliyunConfig(ACCESS_KEY, ACCESS_KEY_SECRET)
    client = AliyunCrypto(config)
    if cache:
        client.crypto_key_manager = CachingCryptoKeyManager(LocalDataKeyMaterialCache(), 5)
    return client


def file_stream_sample():
    origin_file_path = r"some_file"
    encrypted_file_path = r"enc_file"
    decrypted_file_path = r"dec_file"
    provider = DefaultDataKeyProvider(AES_KEY_ARN)
    client = build_aliyun_crypto()
    with open(origin_file_path, "rb") as f, open(encryped_file_path, "wb") as cipher_text:
        encrypted_stream, _ = client.encrypt_stream(provider, f)
        with encrypted_stream as stream:
            for content in stream:
                cipher_text.write(content)

    with open(encryped_file_path, "rb") as f, open(decrypted_file_path, "wb") as plain_text:
        decrypted_stream, _ = client.decrypt_stream(provider, f)
        with decrypted_stream as stream:
            for content in stream:
                plain_text.write(content)


if __name__ == '__main__':
    ACCESS_KEY_ID = os.getenv("ACCESS_KEY_ID")
    ACCESS_KEY_SECRET = os.getenv("ACCESS_KEY_SECRET")
    AES_KEY_ARN = os.getenv("AES_KEY_ARN")
    file_stream_sample()
```

