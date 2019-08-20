# Request structure {#concept_69006_zh .concept}

## Service endpoints {#section_x3t_t3p_kfb .section}

The following table lists the service access endpoints of the KMS API.

|Region|RegionId|Public network endpoint|Private network endpoint|
|:-----|:-------|:----------------------|:-----------------------|
|Asia Pacific NE 1 \(Tokyo\)|ap-northeast-1|kms.ap-northeast-1.aliyuncs.com|kms-vpc.ap-northeast-1.aliyuncs.com|
|Asia Pacific SE 1 \(Singapore\)|ap-southeast-1|kms.ap-southeast-1.aliyuncs.com|kms-vpc.ap-southeast-1.aliyuncs.com|
|Asia Pacific SE 2 \(Sydney\)|ap-southeast-2|kms.ap-southeast-2.aliyuncs.com|kms-vpc.ap-southeast-2.aliyuncs.com|
|Asia Pacific SE 3 \(Kuala Lumpur\)|ap-southeast-3|kms.ap-southeast-3.aliyuncs.com|kms-vpc.ap-southeast-3.aliyuncs.com|
|Asia Pacific SE 5 \(Jakarta\)|ap-southeast-5|kms.ap-southeast-5.aliyuncs.com|kms-vpc.ap-southeast-5.aliyuncs.com|
|Asia Pacific SOU 1 \(Mumbai\)|ap-south-1|kms.ap-south-1.aliyuncs.com|kms-vpc.ap-south-1.aliyuncs.com|
|China East 1 \(Hangzhou\)|cn-hangzhou|kms.cn-hangzhou.aliyuncs.com|kms-vpc.cn-hangzhou.aliyuncs.com|
|China East 2 \(Shanghai\)|cn-shanghai|kms.cn-shanghai.aliyuncs.com|kms-vpc.cn-shanghai.aliyuncs.com|
|China North 1 \(Qingdao\)|cn-qingdao|kms.cn-qingdao.aliyuncs.com|kms-vpc.cn-qingdao.aliyuncs.com|
|China North 2 \(Beijing\)|cn-beijing|kms.cn-beijing.aliyuncs.com|kms-vpc.cn-beijing.aliyuncs.com|
|China North 3 \(Zhangjiakou\)|cn-zhangjiakou|kms.cn-zhangjiakou.aliyuncs.com|kms-vpc.cn-zhangjiakou.aliyuncs.com|
|China North 5 \(Hohhot\)|cn-huhehaote|kms.cn-huhehaote.aliyuncs.com|kms-vpc.cn-huhehaote.aliyuncs.com|
|China South 1 \(Shenzhen\)|cn-shenzhen|kms.cn-shenzhen.aliyuncs.com|kms-vpc.cn-shenzhen.aliyuncs.com|
|EU Central 1 \(Frankfurt\)|eu-central-1|kms.eu-central-1.aliyuncs.com|kms-vpc.eu-central-1.aliyuncs.com|
|Middle East 1 \(Dubai\)|me-east-1|kms.me-east-1.aliyuncs.com|kms-vpc.me-east-1.aliyuncs.com|
|China \(Hong Kong\)|cn-hongkong|kms.cn-hongkong.aliyuncs.com|kms-vpc.cn-hongkong.aliyuncs.com|
|US East 1 \(Virginia\)|us-east-1|kms.us-east-1.aliyuncs.com|kms-vpc.us-east-1.aliyuncs.com|
|US West 1 \(Silicon Valley\)|us-west-1|kms.us-west-1.aliyuncs.com|kms-vpc.us-west-1.aliyuncs.com|
|China East 1 \(Hangzhou finance cloud\)|cn-hangzhou-finance|kms.cn-hangzhou-finance.aliyuncs.com|None|
|China East 2 \(Shanghai finance cloud\)|cn-shanghai-finance-1|kms.cn-shanghai-finance-1.aliyuncs.com|kms-vpc.cn-shanghai-finance-1.aliyuncs.com|
|China South 1 \(Shenzhen finance cloud\)|cn-shenzhen-finance-1|kms.cn-shenzhen-finance-1.aliyuncs.com|kms-vpc.cn-shenzhen-finance-1.aliyuncs.com|
|UK \(London\)|eu-west-1|kms.eu-west-1.aliyuncs.com|kms-vpc.eu-west-1.aliyuncs.com|

## Interaction protocol {#section_cms_ycg_ngo .section}

KMS API requests are HTTPS POST and GET request messages.

SSLv2 and SSLv3 are not supported. TLS1.0 and later versions are supported.

## Request method {#section_42r_wog_ins .section}

A POST or GET request is a URL encoded with the parameter value that the interface you access requires.

## Request parameters {#section_mfq_zyg_lqp .section}

For each request, the operation to be executed, namely, the `Action` parameters \(for example, [CreateKey](reseller.en-US/API Reference/API list/CreateKey.md#)\), must be specified. Each operation must include the [Common parameters](reseller.en-US/API Reference/Calling method/Common parameters.md#) and the specific request parameters of the specified operations.

## Character encoding {#section_yp4_eze_6yb .section}

Requests and returned results are both encoded using `UTF-8`.

