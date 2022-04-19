# modifyVpc


## 描述
修改私有网络


## 请求方式
POST

## 请求地址
https://cps.jdcloud-api.com/v1/regions/{regionId}/vpcs/{vpcId}

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |地域ID，可调用接口（describeRegiones）获取云物理服务器支持的地域|
|**vpcId**|String|True| |私有网络ID|

## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**name**|String|False| |名称|
|**description**|String|False| |描述|


## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](modifyvpc#result)| |
|**requestId**|String| |

### <div id="result">Result</div>
|名称|类型|描述|
|---|---|---|
|**vpc**|[Vpc](modifyvpc#vpc)|私有网络详细信息|
### <div id="vpc">Vpc</div>
|名称|类型|描述|
|---|---|---|
|**region**|String|地域代码, 如cn-north-1|
|**vpcId**|String|私有网络ID|
|**name**|String|私有网络名称|
|**cidr**|String|私有网络IPv4 CIDR|
|**ipv6Cidr**|String|私有网络IPv6 CIDR|
|**ipv6GatewayId**|String|IPv6网关ID|
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
