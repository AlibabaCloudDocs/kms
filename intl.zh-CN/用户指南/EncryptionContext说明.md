# EncryptionContext说明 {#concept_42975_zh .concept}

Encryption Context 是在 KMS 的 Encrypt、GenerateDataKey、Decrypt 这些 API 中可能会用到的 JSON 字符串。

## Encryption Context的作用 {#section_42975_01 .section}

Encryption Context 只能是 String-String 形式的 JSON，用于保护数据的完整性。

当在加密（Encrypt、GenerateDataKey）时指定了该参数时，解密（Decrypt）密文时，需要传入[等价的Encryption Context](#section_42975_03)的参数，才能正确的解密。Encryption Context 虽然与解密相关，但是并不会存在密文（CipherBlob）中。

## Encryption Context有效值 {#section_42975_02 .section}

Encryption Context 的有效值是一个总长度在 8192 个字符数以内的 JSON 字符串，并且只能是 String-String 形式的。 当您直接调用 API 填 Encryption Context 的时候，请注意转义的问题。

有效的Encryption Context示例

``` {#codeblock_1w6_zrs_08f}
{"ValidKey":"ValidValue"}
{"Key1":"Value1","Key2":"Value2"}
			
```

无效的Encryption Context \(部分\)示例

``` {#codeblock_8gl_myk_avi}
[{"Key":"Value"}] //json数组
{"Key":12345} //String-int
{"Key":["value1","value2"]} //String-数组
			
```

## 等价的Encryption Context {#section_42975_03 .section}

Encryption Context的本质是一个 String-String的map（hashtable）, 因此在作为参数时，只需要保证 JSON 字符串所表示的key-value含义是一致的，则 Encryption Context 是等价的。与加密时输入的 Encryption Context 等价的 Encryption Context 就可以用于正确的解密，而不用保持完全一致的字符串。

等价的Encryption Context示例

``` {#codeblock_q80_0bf_7xz}
{"Key1":"Value1","Key2":"Value2"} 与 {"Key2":"Value2","Key1":"Value1"} 等价
			
```

