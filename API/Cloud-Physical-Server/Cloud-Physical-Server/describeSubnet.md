# describeSubnet


## 描述
查询子网详情

## 请求方式
GET

## 请求地址
https://cps.jdcloud-api.com/v1/regions/{regionId}/subnets/{subnetId}

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |地域ID，可调用接口（describeRegiones）获取云物理服务器支持的地域|
|**subnetId**|String|True| |子网ID|

## 请求参数
无


## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](describesubnet#result)| |
|**requestId**|String| |

### <div id="result">Result</div>
|名称|类型|描述|
|---|---|---|
|**subnet**|[Subnet](describesubnet#subnet)|子网详细信息|
### <div id="subnet">Subnet</div>
|名称|类型|描述|
|---|---|---|
|**region**|String|地域代码, 如cn-north-1|
|**az**|String|可用区, 如cn-north-1c|
|**subnetId**|String|子网ID|
|**name**|String|子网名称|
|**cidr**|String|子网ipv4 CIDR|
|**ipv6Cidr**|String|子网IPv6 CIDR|
|**vpcId**|String|私有网络Id|
|**vpcName**|String|私有网络名称|
|**vpcCidr**|String|私有网络IPv4 CIDR|
|**vpcIpv6Cidr**|String|私有网络IPv6 CIDR|
|**availableIpCount**|Integer|可用IPv4地址数量|
|**totalIpCount**|Integer|总IPv4地址数量|
|**usedIpv6IpCount**|Integer|已用IPv6地址数量|
|**totalIpv6IpCount**|String|总IPv6地址数量|
|**secondaryCidrName**|String|子网次要CIDR名称|
|**secondaryCidr**|String|子网次要CIDR|
|**secondaryCidrId**|String|子网次要CIDR ID|
|**networkType**|String|网络类型|
|**description**|String|描述|
|**createTime**|String|创建时间|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
|**400**|Bad request|
|**404**|Not found|
|**500**|Internal server error|
|**503**|Service unavailable|
