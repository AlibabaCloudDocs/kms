# Billing

This topic describes the fees charged for Key Management Service \(KMS\) and provides some billing examples.

## Fees for hosting keys

Customer master keys \(CMKs\) in the Pending Deletion state are not charged. The following table describes billing rules for CMKs in other states.

|Key creator|Billable item|Unit price in Alibaba Cloud regions \(USD/day\)|
|-----------|-------------|-----------------------------------------------|
|Alibaba Cloud service|Version of a service-managed key1|0.0|
|User|Version of a software key2|0.002|
|Version of a basic hardware key3|0.033|
|Version of an advanced hardware key4|-   0.083 for the first 2,000 key versions
-   0.033 for other key versions |

1 A CMK automatically created by an Alibaba Cloud service and managed by an Alibaba Cloud account. For more information, see [Select appropriate keys](/intl.en-US/Integration of Alibaba Cloud Services with KMS/Integration with KMS.md).

2 A CMK whose protection level is `Software`.

3 A CMK whose key type is `Aliyun_AES_256`, `Aliyun_SM4`, or `RSA_2048` and whose protection level is `HSM`.

4 A CMK whose key type is `Aliyun_SM2`, `RSA_3072`, `EC_P256`, or `EC_P256K` and whose protection level is `HSM`.

## Fees for calling API operations

You can make a total number of 20,000 API operation calls free of charge for your service-managed keys in all regions each month. API operation calls for service-managed keys beyond this free quota and API operation calls for user-managed keys are subject to the billing rules listed in the following table.

|Key category|Unit price in Alibaba Cloud regions in mainland China \(USD/10,000 calls\)|Unit price in Alibaba Cloud regions outside mainland China \(USD/10,000 calls\)|
|------------|--------------------------------------------------------------------------|-------------------------------------------------------------------------------|
|Service-managed key1|0.08|0.03|
|Basic key2 \(software and hardware\)|0.08|0.03|
|Advanced key3 \(software and hardware\)|0.24|0.15|

1 A CMK automatically created by an Alibaba Cloud service and managed by an Alibaba Cloud account. For more information, see [Select appropriate keys](/intl.en-US/Integration of Alibaba Cloud Services with KMS/Integration with KMS.md).

2 A CMK whose key type is `Aliyun_AES_256`, `Aliyun_SM4`, or `RSA_2048`.

3 A CMK whose key type is `Aliyun_SM2`, `RSA_3072`, `EC_P256`, or `EC_P256K`.

## Billing example 1: Disk encryption

In the Singapore \(Singapore\) region, 250 disks are created per month. A CMK is used to encrypt the disks.

Fees:

-   Hosted keys: one CMK

    **Note:** The CMK can be a custom hardware key. In this case, you are charged for hosting the CMK. The CMK can also be a service-managed key. In this case, you are charged for calling API operations by using the CMK beyond the monthly free quota of 20,000 calls.

-   API operation calls: 750 \(250 calls to create data keys, 250 calls to encrypt the data keys, and 250 calls to decrypt the data keys\)

The following table lists the estimated monthly costs.

|Fee|Service-managed key \(USD\)|Custom hardware key \(USD\)|
|---|---------------------------|---------------------------|
|Key hosting|0|1|
|API operation calls|0 \(The number of calls is 750, which does not exceed the free quota 20,000.\)|0.002 \(0.03 × 750/10,000\)|
|Total|0|1.002|

## Billing example 2: OSS client-side encryption

In the Singapore \(Singapore\) region, a CMK is used for OSS client-side encryption, which is based on envelope encryption. A total number of 10,000 objects are encrypted and uploaded per month. The encrypted objects are read for 2,000,000 times per month.

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

In the Singapore \(Singapore\) region, a CMK whose key type is `EC_P256` is used to generate 100,000 signatures.

Fees:

-   Hosted keys: one CMK
-   API operation calls: 100,000 calls to generate signatures

The following table lists the estimated monthly costs.

|Fee|Custom hardware key \(USD\)|
|---|---------------------------|
|Key hosting|2.49|
|API operation calls|1.50 \(0.15 × 100,000/10,000\)|
|Total|3.99|

