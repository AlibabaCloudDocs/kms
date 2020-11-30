# EncryptionContext说明

EncryptionContext是在KMS的Encrypt、GenerateDataKey、Decrypt等API中可能用到的JSON字符串。

## EncryptionContext的作用

EncryptionContext只能是String-String形式的JSON字符串，用于保护数据的完整性。

如果加密（Encrypt、GenerateDataKey）时指定了该参数，解密（Decrypt）密文时，需要传入等价的EncryptionContext参数，才能正确的解密。EncryptionContext虽然与解密相关，但是并不会存在密文（CipherBlob）中。

## EncryptionContext有效值

EncryptionContext的有效值是一个总长度在8192个字符数以内的JSON字符串，并且只能是String-String形式。当您直接调用API填写EncryptionContext时，请注意转义问题。

有效的EncryptionContext示例

```
{"ValidKey":"ValidValue"}
{"Key1":"Value1","Key2":"Value2"}
            
```

无效的EncryptionContext（部分）示例

```
[{"Key":"Value"}] //JSON数组
{"Key":12345} //String-int
{"Key":["value1","value2"]} //String-数组
            
```

## 等价的EncryptionContext

EncryptionContext的本质是一个String-String的map（hashtable）, 因此在作为参数时，只需要保证JSON字符串所表示的key-value含义是一致的，则EncryptionContext是等价的。与加密时输入的EncryptionContext等价的EncryptionContext即可用于正确的解密，而不用保持完全一致的字符串。

等价的EncryptionContext示例

```
{"Key1":"Value1","Key2":"Value2"} 与 {"Key2":"Value2","Key1":"Value1"} 等价
            
```

