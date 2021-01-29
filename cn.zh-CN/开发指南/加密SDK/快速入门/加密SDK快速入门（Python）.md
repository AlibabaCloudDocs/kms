# 加密SDK快速入门（Python）

加密SDK（Encryption SDK）是一个客户端密码库，通过与密钥管理服务KMS（Key Management Service）结合使用，帮助您快速实现数据的加解密、签名验签功能。本文以Python语言为例，为您介绍如何快速使用加密SDK进行数据加解密。

## 对字节数组类型的数据进行加解密

```
import base64
from aliyun_encryption_sdk.cache.local import LocalDataKeyMaterialCache
from aliyun_encryption_sdk.ckm.cache import CachingCryptoKeyManager
from aliyun_encryption_sdk.client import AliyunCrypto
from aliyun_encryption_sdk.kms import AliyunConfig
from aliyun_encryption_sdk.provider.default import DefaultDataKeyProvider
from examples.src.sample_secret import AES_KEY_ID, ACCESS_KEY, ACCESS_KEY_SECRET, ENCRYPTION_CONTEXT

PLAIN_TEXT = "test_plain_text"


def build_aliyun_crypto(cache=False):
    config = AliyunConfig(ACCESS_KEY, ACCESS_KEY_SECRET)
    client = AliyunCrypto(config)
    if cache:
        client.crypto_key_manager = CachingCryptoKeyManager(LocalDataKeyMaterialCache(), 5)
    return client


def encrypt_sample():
    print("原文: " + PLAIN_TEXT)
    provider = DefaultDataKeyProvider(AES_KEY_ID)
    client = build_aliyun_crypto(False)
    cipher_text, enc_material = client.encrypt(provider, bytes(PLAIN_TEXT, "utf-8"), ENCRYPTION_CONTEXT)
    cipher_text_str = base64.encodebytes(cipher_text).decode()
    print("加密密文: " + cipher_text_str)
    return cipher_text_str


def decrypt_sample(cipher_text):
    cipher_text_bytes = base64.decodebytes(cipher_text.encode())
    provider = DefaultDataKeyProvider(AES_KEY_ID)
    client = build_aliyun_crypto(False)
    plain_text, dec_material = client.decrypt(provider, cipher_text_bytes)
    print("解密结果: " + bytes.decode(plain_text))
    return plain_text


if __name__ == '__main__':
    cipherText = encrypt_sample()
    decrypt_sample(cipherText)
```

## 对字节流类型的数据进行加解密

```
from aliyun_encryption_sdk.cache.local import LocalDataKeyMaterialCache
from aliyun_encryption_sdk.ckm.cache import CachingCryptoKeyManager
from aliyun_encryption_sdk.client import AliyunCrypto
from examples.src.sample_secret import AES_KEY_ID, ACCESS_KEY, ACCESS_KEY_SECRET
from aliyun_encryption_sdk.kms import AliyunConfig
from aliyun_encryption_sdk.provider.default import DefaultDataKeyProvider


def build_aliyun_crypto(cache=False):
    config = AliyunConfig(ACCESS_KEY, ACCESS_KEY_SECRET)
    client = AliyunCrypto(config)
    if cache:
        client.crypto_key_manager = CachingCryptoKeyManager(LocalDataKeyMaterialCache(), 5)
    return client


def file_stream_sample():
    file_path = r"..\test_file"
    provider = DefaultDataKeyProvider(AES_KEY_ID)
    client = build_aliyun_crypto()
    with open(file_path + r"\test.txt", "rb") as f, open(file_path + r"\test_enc.enc", "wb") as cipher_text:
        encrypted_stream, _ = client.encrypt_stream(provider, f)
        with encrypted_stream as stream:
            for content in stream:
                cipher_text.write(content)

    with open(file_path + r"\test_enc.enc", "rb") as f, open(file_path + r"\test_dec.txt", "wb") as plain_text:
        decrypted_stream, _ = client.decrypt_stream(provider, f)
        with decrypted_stream as stream:
            for content in stream:
                plain_text.write(content)


if __name__ == '__main__':
    file_stream_sample()
```

