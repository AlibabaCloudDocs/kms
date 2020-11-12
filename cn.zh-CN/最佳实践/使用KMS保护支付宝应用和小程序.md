# 使用KMS保护支付宝应用和小程序

在支付宝开放平台的应用体系中，应用私钥是最核心的安全要素，使用密钥管理服务KMS（Key Management Service）保护私钥，可以极大的提高支付宝应用和小程序的安全性，帮助应用开发者保障业务和资金安全。

## 背景信息

支付宝开放平台的应用管理体系采用公私钥的机制，以保障商户应用和支付宝交互的安全性。这一机制包括以下两部分：

-   商户应用使用自己的私钥对消息加签后，将消息和签名传递给支付宝，支付宝则使用应用的公钥验证消息的真实性（来自于合法应用的真实消息）。

    ![支付宝机制](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0078428951/p143524.png)

-   对于支付宝返回消息给商户应用的情形，应用则使用支付宝的平台公钥来验证返回消息的真实性。

该机制的前提是：商户应用必须保障应用私钥的安全性，从而保障应用和和支付宝交互的安全性。反之，一旦私钥发生泄露，商户会面临较大的安全风险。如果应用和支付宝的交互涉及到资金类接口则风险更大。

## 产品价值

相比于在应用中使用应用私钥的明文来对消息进行加签，KMS存在以下优势：

-   保障私钥安全性：用户可以将签名私钥安全存放在KMS托管密码机内。用户通过KMS的OpenAPI使用私钥加签时，私钥会在密码机的硬件安全边界之内，完成运算后返回签名值，从而防止私钥的泄露。托管密码机详情，请参见[托管密码机概述](/cn.zh-CN/密钥服务/托管密码机/托管密码机概述.md)。
-   控制私钥使用者：用户可以通过阿里云访问控制RAM（Resource Access Management），集中管控KMS密钥使用成员，用于应用加签。
-   审计对私钥的调用日志：通过阿里云操作审计（ActionTrail）可以查看每一次调用KMS的记录；而商家应用自行保管私钥则很难产生客观的审计事件。
-   灵活响应安全事件：在应用系统遭遇恶意者攻击等情形下，可以通过多种手段阻止恶意者对私钥的非法使用。例如：用户可以通过RAM撤销对私钥的使用权限，或者通过KMS禁用私钥等。

![KMS价值](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1078428951/p143805.png)

## 使用KMS控制台为支付宝应用或小程序加签

1.  在KMS中创建密钥。

    1.  登录[密钥管理服务控制台](https://kms.console.aliyun.com)。

    2.  在页面左上角的地域下拉列表，选择密钥所在的地域。

        建议您选择和支付宝应用或小程序相同的地域。

    3.  在左侧导航栏，单击**用户主密钥**。

    4.  单击**创建密钥**。

    5.  在弹出的创建密钥对话框，根据以下表格进行配置。

        |配置项|说明|
        |---|--|
        |**密钥类型**|选择**RSA\_2048**。|
        |**密钥用途**|选择**Sign/Verify**。|
        |**保护级别**|选择**Hsm**：通过KMS系统的硬件加密机产生和保护密钥。|
        |**描述**|输入密钥描述信息。|
        |**轮转周期**|默认为**不开启**。|

    6.  单击**确认**。

2.  在支付宝配置密钥。

    支付宝开放平台提供了普通公钥方式和公钥证书方式两种密钥配置方法。公钥证书方式是对普通公钥方式的增强机制，从数字签名的角度来看，二者机制大同小异，商户应用只需要选择其中一种即可。

    **说明：** 对于涉及到资金往来的商户应用，应当使用公钥证书的方式。

    -   **方法一：普通公钥方式**

        从KMS获取应用公钥，注册到支付宝开放平台对应的应用中。

        1.  登录[密钥管理服务控制台](https://kms.console.aliyun.com)。
        2.  在页面左上角的地域下拉列表，选择密钥所在的地域。
        3.  在左侧导航栏，单击**用户主密钥**。
        4.  找到已创建的RSA\_2048类型密钥，单击别名进入详情页。
        5.  在**密钥版本**区域，单击**查看公钥**。
        6.  在弹出的查看公钥对话框，复制或下载公钥。
        7.  登录[支付宝开放平台](https://mini.open.alipay.com/channel/miniIndex.htm)。
        8.  打开需要加密的应用，在左侧导航栏单击**开发设置**，并单击**开发设置**页签。
        9.  在**开发设置**页签，单击接口加密方式右侧的**设置**，在弹出的对话框输入手机验证码进行验证。
        10. 在加密管理对话框择选择加签模式为**公钥**，在**填写公钥字符**区域输入公钥，单击**保存设置**完成公钥的配置。

            ![加签](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1078428951/p141498.png)

    -   **方法二：公钥证书方式**

        从KMS获取私钥证书请求CSR，到支付宝开放平台完成应用证书注册和签发。

        1.  登录[密钥管理服务控制台](https://kms.console.aliyun.com)。
        2.  在页面左上角的地域下拉列表，选择密钥所在的地域。
        3.  在左侧导航栏，单击**用户主密钥**。
        4.  找到已创建的RSA\_2048类型密钥，单击别名进入详情页。
        5.  在**密钥版本**区域，单击**生成CSR**。
        6.  在弹出的生成CSR对话框，根据控制台提示填写证书信息。

            **说明：** **企业/单位名称**必须和支付宝开发者中心门户账号信息的公司名称保持一致，否则会导致后续步骤中上传CSR证书文件校验失败。

            ![CSR](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1078428951/p141510.png)

        7.  登录[支付宝开放平台](https://mini.open.alipay.com/channel/miniIndex.htm)。
        8.  打开需要加密的应用，在左侧导航栏单击**开发设置**，并单击**开发设置**页签。
        9.  在**开发设置**页签，单击接口加密方式右侧的**设置**，在弹出的对话框输入手机验证码进行验证。
        10. 在加密管理对话框选择加签模式为**公钥证书**，在**上传证书文件**区域单击**上传CSR文件在线生成证书**。

            ![公钥证书](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1078428951/p141515.png)

        11. 单击**上传CSR文件在线生成证书**上传公钥证书，完成公钥证书的设置。

## 使用支付宝SDK调用KMS为支付宝应用或小程序加签

支付宝开放平台新版SDK（EasySDK）集成了KMS作为加签提供器（Sign Provider），以简化加签操作。以Java SDK为例，您需要在支付宝应用中引用EasySDK 2.0.1以及之后的版本。

```
<dependency>
    <groupId>com.alipay.sdk</groupId>
    <artifactId>alipay-easysdk</artifactId>
    <version>2.0.1</version>
</dependency>
```

**说明：** 如果遵循[支付宝开放API的签名规则](https://opendocs.alipay.com/open/291/106118)，也可以不使用EasySDK，通过调用阿里云KMS的[AsymmetricSign](/cn.zh-CN/API参考/密钥/AsymmetricSign.md)接口自行实现签名。

**代码示例：普通公钥方式**

```
package com.aliyun.kms.samples;

import com.alipay.easysdk.base.qrcode.models.AlipayOpenAppQrcodeCreateResponse;
import com.alipay.easysdk.factory.Factory;
import com.alipay.easysdk.kms.aliyun.AliyunKMSConfig;
import com.google.gson.Gson;
import com.google.gson.reflect.TypeToken;

import java.io.InputStream;
import java.io.InputStreamReader;
import java.util.Map;

/**
 * Alipay-easysdk使用KMS签名示例，本示例展示了公钥方式调用。
 */
public class KmsAlipayEasySDKPublicKeyDemo {
    public static void main(String[] args) {
        Factory.setOptions(getOptions());
        try {
            AlipayOpenAppQrcodeCreateResponse response = Factory.Base.Qrcode().create("page/component/component-pages/view/view", "x=1", "二维码描述");
            if ("10000".equals(response.code)) {
                System.out.println("调用成功");
            } else {
                System.err.println("调用失败，原因：" + response.msg + "，" + response.subMsg);
            }
        } catch (Exception e) {
            System.err.println("调用遭遇异常，原因：" + e.getMessage());
            throw new RuntimeException(e.getMessage(), e);
        }
    }

    private static AliyunKMSConfig getOptions() {
        AliyunKMSConfig config = new AliyunKMSConfig();
        config.protocol = "https";
        config.gatewayHost = "openapi.alipay.com";
        config.signType = "RSA2";

        //请更换为您的AppID。
        config.appId = "202100****";
        //请修改如下的支付宝公钥字符串为自己的支付宝公钥。
        config.alipayPublicKey = "MIIBIjANB...";

        //如果使用阿里云KMS签名，则需要指定签名提供方名称，阿里云KMS的名称为"AliyunKMS"。
        config.signProvider = "AliyunKMS";

        //如果使用阿里云KMS签名，请更换为您的阿里云AccessKey ID。
        config.aliyunAccessKeyId = getAliyunAccessKey("AccessKeyId");
        //如果使用阿里云KMS签名，请更换为您的阿里云AccessKey Secret。
        config.aliyunAccessKeySecret = getAliyunAccessKey("AccessKeySecret");
        //如果使用阿里云KMS签名，请更换为您的KMS服务密钥ID。
        config.kmsKeyId = "4358f298-8e30-4849-9791-****";
        //如果使用阿里云KMS签名，请更换为您的KMS服务密钥版本ID。
        config.kmsKeyVersionId = "e71daa69-c321-4014-b0c4-****";

        //如果使用阿里云KMS签名，需要更换为您的KMS服务地址。
        //KMS服务地址列表详情，请参考：
        //https://help.aliyun.com/document_detail/69006.html
        config.kmsEndpoint = "kms.cn-hangzhou.aliyuncs.com";

        return config;
    }

    /**
     * 从文件中读取阿里云AccessKey配置信息。
     * 此处为了测试执行的环境普适性，AccessKey信息配置在resources资源下，实际过程中请不要这样配置。
     *
     * @param key AccessKey配置对应的key。
     * @return AccessKey配置字符串。
     */
    private static String getAliyunAccessKey(String key) {
        InputStream stream = KmsAlipayEasySDKPublicKeyDemo.class.getResourceAsStream("/fixture/aliyunAccessKey.json");
        Map<String, String> result = new Gson().fromJson(new InputStreamReader(stream), new TypeToken<Map<String, String>>() {
        }.getType());
        return result.get(key);
    }
}
```

**代码示例：公钥证书方式**

使用公钥证书方式时，EasySDK的使用方式和上述示例类似，区别主要在于配置了商户应用和支付宝平台的公钥证书。更多信息，请参见[阿里云KMS Github代码样例库](https://github.com/aliyun/alibabacloud-kms-demo/blob/master/kms-samples-java/src/main/java/com/aliyun/kms/samples/KmsAlipayEasySDKCertDemo.java?spm=a2c6h.12873639.0.0.516a7f784D84Xp&file=KmsAlipayEasySDKCertDemo.java)。

