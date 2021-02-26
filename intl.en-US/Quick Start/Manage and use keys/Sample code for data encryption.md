# Sample code for data encryption

After you create a customer master key \(CMK\) of the Advanced Encryption Standard \(AES\) or SM4 type, you can use code of Key Management Service \(KMS\) SDKs to encrypt data. In the example provided in this topic, KMS SDK for Java is used to encrypt data.

## Preparations

1.  Obtain the dependency declaration of KMS SDK for Java. For information about the required SDK version, see [SDK overview](/intl.en-US/Developer Guide/KMS SDK/SDK overview.md). Sample code:

    ```
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>4.5.2</version>
    </dependency>
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-kms</artifactId>
        <version>2.14.0</version>
    </dependency>
    ```

2.  Obtain the endpoints to access KMS based on the region where you use KMS. For more information, see [Endpoints](/intl.en-US/API Reference/Calling method/Request syntax.md).

    **Note:** In this example, you can specify the region ID to access the public endpoint of KMS. For more information about how to access the Virtual Private Cloud \(VPC\) endpoint of KMS, see [Code samples of SDK for Java](/intl.en-US/Developer Guide/KMS SDK/Code samples of SDK for Java.md).


## Encrypt data

Use the following code of KMS SDK for Java to encrypt data:

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.kms.model.v20160120.*;
import com.aliyuncs.utils.Base64Helper;

public class Encrypt {

    public static void main(String[] args) {
        /* 
         * 1. Specify the region where your CMK resides.
         * 2. Specify the AccessKey ID and AccessKey secret that are required to access KMS.
        */
        DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        EncryptRequest request = new EncryptRequest();
        
        // Specify the CMK alias or CMK ID that is used to encrypt "Hello world".
        request.setKeyId("alias/Apollo/SalaryEncryptionKey");
        request.setPlaintext(Base64Helper.encode("Hello world", null));

        try {
            EncryptResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }
    }
}
```

For more information about the sample code, visit [alibabacloud-kms-demo](https://github.com/aliyun/alibabacloud-kms-demo).

