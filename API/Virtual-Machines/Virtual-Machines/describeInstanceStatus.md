# describeInstanceStatus


## 描述

查询一台或多台云主机实例的状态。

云主机实例的状态说明请参考帮助文档：[云主机状态](https://docs.jdcloud.com/cn/virtual-machines/api/vm_status)

## 接口说明
- 使用 `filters` 过滤器进行条件筛选，每个 `filter` 之间的关系为逻辑与（AND）的关系。
- 单次查询最大可查询100条云主机状态。
- 尽量一次调用接口查询多条数据，不建议使用该批量查询接口一次查询一条数据，如果使用不当导致查询过于密集，可能导致网关触发限流。
- 由于该接口为 `GET` 方式请求，最终参数会转换为 `URL` 上的参数，但是 `HTTP` 协议下的 `GET` 请求参数长度是有大小限制的，使用者需要注意参数超长的问题。


## 请求方式
GET

## 请求地址
https://vm.jdcloud-api.com/v1/regions/{regionId}/instanceStatus

|名称|类型|是否必需|示例值|描述|
|---|---|---|---|---|
|**regionId**|String|是|cn-north-1|地域ID。|

## 请求参数
|名称|类型|是否必选|示例值|描述|
|---|---|---|---|---|
|**pageNumber**|Integer|否| |页码；默认为1。|
|**pageSize**|Integer|否| |分页大小；<br>默认为20；取值范围[10, 100]。|
|**filters**|[Filter[]](describeInstanceStatus#user-content-filter)|否| |<b>filters 中支持使用以下关键字进行过滤</b><br>`instanceId`: 云主机ID，精确匹配，支持多个<br>`privateIpAddress`: 主网卡内网主IP地址，模糊匹配，支持多个<br>`vpcId`: 私有网络ID，精确匹配，支持多个<br>`status`: 云主机状态，精确匹配，支持多个，参考 [云主机状态](https://docs.jdcloud.com/virtual-machines/api/vm_status)<br>`name`: 云主机名称，模糊匹配，支持单个<br>`imageId`: 镜像ID，精确匹配，支持多个<br>`networkInterfaceId`: 弹性网卡ID，精确匹配，支持多个<br>`subnetId`: 子网ID，精确匹配，支持多个<br>|

### <div id="user-content-filter">Filter</div>
|名称|类型|是否必选|示例值|描述|
|---|---|---|---|---|
|**name**|String|是| |过滤条件的名称|
|**operator**|String|否| |过滤条件的操作符，默认eq|
|**values**|String[]|是| |过滤条件的值|

## 返回参数
|名称|类型|示例值|描述|
|---|---|---|---|
|**result**|[Result](describeInstanceStatus#user-content-result)| |响应结果。|
|**requestId**|String|c2hmmaan8w06w19qcdfuic4w03f7ft2d|请求ID。|

### <div id="#user-content-result">Result</div>
|名称|类型|示例值|描述|
|---|---|---|---|
|**instanceStatuses**|[InstanceStatus[]](describeInstanceStatus#user-content-instancestatus)| |云主机实例状态列表。|
|**totalCount**|Number| |本次查询可匹配到的总记录数，使用者需要结合 `pageNumber` 和 `pageSize` 计算是否可以继续分页。|
### <div id="user-content-instancestatus">InstanceStatus</div>
|名称|类型|示例值|描述|
|---|---|---|---|
|**instanceId**|String|i-eumm****d6|云主机ID。|
|**status**|String|running|云主机状态，参考 [云主机状态](https://docs.jdcloud.com/virtual-machines/api/vm_status)。|


## 请求示例
GET

```
/v1/regions/cn-north-1/instanceStatus?pageNumber=1&pageSize=10&filters.1.name=instanceId&filters.1.values.1=i-eumm****d6&filters.1.values.2=i-y5nh****9w
```



## 返回示例
```
{
    "requestId": "b878d51747062fc1621394e974fe635a", 
    "result": {
        "instanceStatuses": [
            {
                "instanceId": "i-eumm****d6", 
                "status": "stopped"
            }, 
            {
                "instanceId": "i-y5nh****9w", 
                "status": "running"
            }
        ], 
        "totalCount": 2
    }
}
```

## 返回码
|HTTP状态码|错误码|描述|错误解析|
|---|---|---|---|
|**200**||OK||
|**400**|OUT_OF_RANGE|PageSize out of range|分页大小超出范围。|
|**500**|INTERNAL|Internal server error|系统内部错误，请稍后重试。如果多次尝试失败，请提交工单。|
|**500**|UNKNOWN|Unknown server error|服务暂时不可用，请稍后重试。如果多次尝试失败，请提交工单。|
