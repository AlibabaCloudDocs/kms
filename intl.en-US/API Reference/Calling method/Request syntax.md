# Request syntax

This topic describes the endpoints, protocols, HTTPS request methods, and request parameters of the Key Management Service \(KMS\) API.

## Endpoints

The following table describes the endpoints of the KMS API.

|Region|RegionId|Public endpoint|VPC endpoint|
|:-----|:-------|:--------------|:-----------|
|Japan \(Tokyo\)|ap-northeast-1|kms.ap-northeast-1.aliyuncs.com|kms-vpc.ap-northeast-1.aliyuncs.com|
|Singapore|ap-southeast-1|kms.ap-southeast-1.aliyuncs.com|kms-vpc.ap-southeast-1.aliyuncs.com|
|Australia \(Sydney\)|ap-southeast-2|kms.ap-southeast-2.aliyuncs.com|kms-vpc.ap-southeast-2.aliyuncs.com|
|Malaysia \(Kuala Lumpur\)|ap-southeast-3|kms.ap-southeast-3.aliyuncs.com|kms-vpc.ap-southeast-3.aliyuncs.com|
|Indonesia \(Jakarta\)|ap-southeast-5|kms.ap-southeast-5.aliyuncs.com|kms-vpc.ap-southeast-5.aliyuncs.com|
|India \(Mumbai\)|ap-south-1|kms.ap-south-1.aliyuncs.com|kms-vpc.ap-south-1.aliyuncs.com|
|China \(Hangzhou\)|cn-hangzhou|kms.cn-hangzhou.aliyuncs.com|kms-vpc.cn-hangzhou.aliyuncs.com|
|China \(Shanghai\)|cn-shanghai|kms.cn-shanghai.aliyuncs.com|kms-vpc.cn-shanghai.aliyuncs.com|
|China \(Qingdao\)|cn-qingdao|kms.cn-qingdao.aliyuncs.com|kms-vpc.cn-qingdao.aliyuncs.com|
|China \(Beijing\)|cn-beijing|kms.cn-beijing.aliyuncs.com|kms-vpc.cn-beijing.aliyuncs.com|
|China \(Zhangjiakou\)|cn-zhangjiakou|kms.cn-zhangjiakou.aliyuncs.com|kms-vpc.cn-zhangjiakou.aliyuncs.com|
|China \(Hohhot\)|cn-huhehaote|kms.cn-huhehaote.aliyuncs.com|kms-vpc.cn-huhehaote.aliyuncs.com|
|China \(Ulanqab\)|cn-wulanchabu|kms.cn-wulanchabu.aliyuncs.com|kms-vpc.cn-wulanchabu.aliyuncs.com|
|China \(Shenzhen\)|cn-shenzhen|kms.cn-shenzhen.aliyuncs.com|kms-vpc.cn-shenzhen.aliyuncs.com|
|China \(Heyuan\)|cn-heyuan|kms.cn-heyuan.aliyuncs.com|kms-vpc.cn-heyuan.aliyuncs.com|
|China \(Guangzhou\)|cn-guangzhou|kms.cn-guangzhou.aliyuncs.com|kms-vpc.cn-guangzhou.aliyuncs.com|
|China \(Chengdu\)|cn-chengdu|kms.cn-chengdu.aliyuncs.com|kms-vpc.cn-chengdu.aliyuncs.com|
|Germany \(Frankfurt\)|eu-central-1|kms.eu-central-1.aliyuncs.com|kms-vpc.eu-central-1.aliyuncs.com|
|UK \(London\)|eu-west-1|kms.eu-west-1.aliyuncs.com|kms-vpc.eu-west-1.aliyuncs.com|
|UAE \(Dubai\)|me-east-1|kms.me-east-1.aliyuncs.com|kms-vpc.me-east-1.aliyuncs.com|
|China \(Hong Kong\)|cn-hongkong|kms.cn-hongkong.aliyuncs.com|kms-vpc.cn-hongkong.aliyuncs.com|
|US \(Virginia\)|us-east-1|kms.us-east-1.aliyuncs.com|kms-vpc.us-east-1.aliyuncs.com|
|US \(Silicon Valley\)|us-west-1|kms.us-west-1.aliyuncs.com|kms-vpc.us-west-1.aliyuncs.com|
|China East 1 Finance|cn-hangzhou-finance|kms.cn-hangzhou-finance.aliyuncs.com|N/A|
|China East 2 Finance|cn-shanghai-finance-1|kms.cn-shanghai-finance-1.aliyuncs.com|kms-vpc.cn-shanghai-finance-1.aliyuncs.com|
|China South 1 Finance|cn-shenzhen-finance-1|kms.cn-shenzhen-finance-1.aliyuncs.com|kms-vpc.cn-shenzhen-finance-1.aliyuncs.com|

## Protocols

You must call KMS API operations by sending HTTPS requests.

KMS does not support Secure Sockets Layer \(SSL\) 2.0 or SSL 3.0. KMS supports only Transport Layer Security \(TLS\) 1.0 and later.

## Request methods

You can call KMS API operations by sending HTTPS POST and GET requests. The request parameters must be included in the request URL.

## Request parameters

Each request must specify the operation to be performed. For example, to create a customer master key \(CMK\), you must set the `Action` parameter to CreateKey. Request parameters include common request parameters and operation-specific parameters.

For more information about common request parameters, see [Common parameters](/intl.en-US/API Reference/Calling method/Common parameters.md).

## Character encoding

All requests and responses are encoded in `UTF-8`.

