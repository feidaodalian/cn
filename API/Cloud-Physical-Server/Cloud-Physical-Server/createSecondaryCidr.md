# createSecondaryCidr


## 描述
添加次要CIDR

## 请求方式
PUT

## 请求地址
https://cps.jdcloud-api.com/v1/regions/{regionId}/secondaryCidrs

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |地域ID，可调用接口（describeRegions）获取云物理服务器支持的地域|

## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**clientToken**|String|False| |由客户端生成，用于保证请求的幂等性，长度不能超过36个字符；<br/><br>如果多个请求使用了相同的clientToken，只会执行第一个请求，之后的请求直接返回第一个请求的结果<br/><br>|
|**secondaryCidrSpec**|[SecondaryCidrSpec](createsecondarycidr#secondarycidrspec)|True| |次要cidr配置|

### <div id="secondarycidrspec">SecondaryCidrSpec</div>
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**subnetId**|String|False| |子网ID|
|**cidr**|String|False| |子网的次要CIDR|
|**name**|String|False| |名称|

## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](createsecondarycidr#result)| |
|**requestId**|String| |

### <div id="result">Result</div>
|名称|类型|描述|
|---|---|---|
|**secondaryCidrId**|String|次要cidr的ID|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
|**400**|Bad request|
|**404**|Not found|
|**500**|Internal server error|
|**503**|Service unavailable|
