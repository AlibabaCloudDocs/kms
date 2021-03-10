# Billing

This topic describes the fees charged for Key Management Service \(KMS\) and provides some billing examples.

## Key hosting fees

Customer master keys \(CMKs\) in the Pending Deletion state are not billed. The following table describes billing rules for CMKs in other states.

|Key creator|Billing item|Unit price in Alibaba Cloud regions \(USD/day\)|
|-----------|------------|-----------------------------------------------|
|Alibaba Cloud service|Version of a service-managed key ①|0.0|
|User|Version of a software key ②|0.002|
|Version of a basic hardware key ③|0.033|
|Version of an advanced hardware key ④|-   0.083 for the first 2,000 key versions
-   0.033 for other key versions |

①A CMK automatically created by an Alibaba Cloud service and managed by an Alibaba Cloud account. For more information, see [Select appropriate keys](/intl.en-US/Integration of Alibaba Cloud Services with KMS/Integration with KMS.md).

②A CMK whose protection level is `Software`.

③A CMK whose key type is `Aliyun_AES_256`, `Aliyun_SM4`, or `RSA_2048` and whose protection level is `HSM`.

④A CMK whose key type is `Aliyun_SM2`, `RSA_3072`, `EC_P256`, or `EC_P256K` and whose protection level is `HSM`.

## API operation call fees

You can make a total number of 20,000 API operation calls free of charge for your service-managed keys in all regions each month. API operation calls for service-managed keys beyond this free quota and API operation calls for user-managed keys are subject to the billing rules listed in the following table.

|Key category|Unit price in regions in mainland China \(USD/10,000 calls\)|Unit price in regions outside mainland China \(USD/10,000 calls\)|
|------------|------------------------------------------------------------|-----------------------------------------------------------------|
|Service-managed key ①|0.08|0.03|
|Basic key ②\(software and hardware\)|0.08|0.03|
|Advanced key ③\(software and hardware\)|0.24|0.15|

①A CMK automatically created by an Alibaba Cloud service and managed by an Alibaba Cloud account. For more information, see [Select appropriate keys](/intl.en-US/Integration of Alibaba Cloud Services with KMS/Integration with KMS.md).

②A CMK whose key type is `Aliyun_AES_256`, `Aliyun_SM4`, or `RSA_2048`.

③A CMK whose key type is `Aliyun_SM2`, `RSA_3072`, `EC_P256`, or `EC_P256K`.

## Billing example 1: Disk encryption

In the Singapore region, 250 disks are created per month. A CMK is used to encrypt the disks.

Fees:

-   Hosted keys: one CMK
-   API operation calls: 750 \(250 calls to create data keys, 250 calls to encrypt the data keys, and 250 calls to decrypt the data keys\)

The following table lists the estimated monthly costs.

|Fee|Service-managed key \(USD\)|Custom hardware key \(USD\)|
|---|---------------------------|---------------------------|
|Key hosting|0|1|
|API operation calls|0 \(The number of calls is 750, which does not exceed the free quota 20,000.\)|0.002 \(0.03 × 750/10,000\)|
|Total|0|1.002|

## Billing example 2: OSS client-side encryption

In the Singapore region, a CMK is used for OSS client-side encryption, which is based on envelope encryption. A total number of 10,000 objects are encrypted and uploaded per month. The encrypted objects are read for 2,000,000 times per month.

Fees:

-   Hosted keys: one CMK
-   API operation calls: 10,000 calls to create data keys \(one call for each object to be uploaded\)
-   API operation calls: 2,000,000 calls to decrypt data keys

The following table lists the estimated monthly costs.

|Fee|Custom hardware key \(USD\)|
|---|---------------------------|
|Key hosting|1|
|API operation calls|6.03 \(0.03 × 2,010,000/10,000\)|
|Total|7.03|

## Billing example 3: Signature generation

In the Singapore region, a CMK whose key type is `EC_P256` is used to generate 100,000 signatures.

Fees:

-   Hosted keys: one CMK
-   API operation calls: 100,000 calls to generate signatures

The following table lists the estimated monthly costs.

|Fee|Custom hardware key \(USD\)|
|---|---------------------------|
|Key hosting|2.49|
|API operation calls|1.50 \(0.15 × 100,000/10,000\)|
|Total|3.99|

