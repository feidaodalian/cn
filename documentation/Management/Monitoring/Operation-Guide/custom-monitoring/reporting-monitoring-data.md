# 上报监控数据
自定义监控功能为您提供上报监控数据的接口，方便您将自己采集的时序数据上报到云监控。目前支持OpenAPI和命令行工具CLI的方式进行上报。  
## OpenAPI上报

### 上报接口描述

1. 接口名称：putMetricData

2. 公网域名  

地域 | 域名
---|---
华北-北京 |monitor.cn-north-1.jdcloud-api.com
华南-广州 |monitor.cn-south-1.jdcloud-api.com
华东-宿迁 |monitor.cn-east-1.jdcloud-api.com
华东-上海 |monitor.cn-east-2.jdcloud-api.com

3. 内网域名  

地域 | 域名
---|---
华北-北京 |monitor.internal.cn-north-1.jdcloud-api.com
华南-广州 |monitor.internal.cn-south-1.jdcloud-api.com
华东-宿迁 |monitor.internal.cn-east-1.jdcloud-api.com
华东-上海 |monitor.internal.cn-east-2.jdcloud-api.com

4.  支持批量上报方式。单次请求最多包含 50 个数据点；数据大小不超过 256k。

注：OpenAPI入门使用请参看<a href="http://docs.jdcloud.com/cn/common-declaration/api/introduction">公共说明</a>

### 请求方式

POST   https://{域名}/v1/customMetrics

例如： POST    https://monitor.cn-north-1.jdcloud-api.com/v1/customMetrics

### 请求参数

名称 | 类型 | 是否必选 | 描述
---|---|---|---
metricDataList|	MetricDataCm[] |	False |	数据参数   

#### MetricDataCm

名称 | 类型 | 是否必选 | 描述
---|---|---|---
dimensions|Object |True|数据维度，数据类型为map类型，支持最少一个，最多五个标签，总长度不大于255字节，只允许英文、数字、下划线_、点., [0-9][a-z] [A-Z] [. _ ]，  其它会返回err
metric|	String |True |	监控指标名称，长度不超过255字节，只允许英文、数字、下划线_、点.,  [0-9][a-z] [A-Z] [. _ ]， 其它会返回err               
namespace |	String|	True|命名空间 ，长度不超过255字节，只允许英文、数字、下划线_、点., [0-9][a-z] [A-Z] [. _ ]，  其它会返回err               
timestamp|Integer|True|上报数据点的时间戳,只支持10位，秒级时间戳，不能写入过去30天的时间                              
type |Integer|True |数据类型，当前仅支持输入值1，表示原始数据。                          
values |	Object | True |指标值集合，数据类型必须为map类型，key为数据类型，value为数据值，当前仅支持type=1，且key只能为”value”。 
unit | String |False |数据的单位，长度不超过64字节，只允许英文、数字、下划线_、点., [0-9][a-z] [A-Z] [. _ ]， 其它会返回err

### 返回参数  

名称 | 类型 | 是否必选 
---|---|---
error |Object| 错误信息 。     
requestId|String |请求的标识id                        
result |Result |                
                      
#### Result
名称 | 类型 | 是否必选 
---|---|---
errMetricDataList|MetricDataList[]|
success|Boolean  |全部写入成功为true，否则为false   

#### MetricDataList
名称 | 类型 | 是否必选 
---|---|---
errDetail|string	| 错误数据描述
errMetricData |string |错误数据              

### 返回码  
名称 | 类型 
---|---
200	|OK
400	|invalid parameter
500 |internal server error
429	|quota exceed


### 示例代码

注：直接使用该示例时，请替换timestamp参数为最新的10位秒级时间戳，否则会写入失败（禁止写入时间戳超过过去30天的数据）。  

请求示例
```
{
	"metricDataList": [
	  {
			"namespace": "test",
			"metric": "vm.mem.usage1",
			"dimensions": {
				"host": "1.2.3.23",
				"datacenter": "cn-north-1"
			},
			"timestamp": 1552446075,
			"type": 1,
			"values": {
				"value": "12342213"
			}
		},

		{
			"namespace": "test1",
			"metric": "vm.cpu.usage",
			"dimensions": {
				"host": "1.2.3.19",
				"tag": "bj"
			},
			"timestamp": 1552446075,
			"type": 2,
			"values": {
				"value": "12342213"
			}
		}
	]
}
```

#### 返回示例

```
success：

{
    "requestId": "1111",
    "result": {
        "success": true,
        "errMetricDataList": []
    }
}

fail：
{
	"requestId": "1111",
	"result": {
		"success": false,
		"errMetricDataList": [{
			"ErrMetricData": "{\"namespace\":\"test1\",\"metric\":\"vm.cpu.usage\",\"dimensions\":{\"host\":\"1.2.3.19\",\"region\":\"bj\",\"tag\":\"bj\",\"tag2\":\"bj\",\"tag3\":\"bj\",\"tag4\":\"bj\"},\"timestamp\":1540361379,\"type\":2,\"values\":{\"avg\":\"80\",\"max\":\"32424244120\"}}",
			"errDetail": "Invalid dimensions,dimensions num limited in 1 to 5 and not null"
		}]
	},
	"error": {
		"code": 400,
		"message": "INVALID_ARGUMENT",
		"status": "INVALID_ARGUMENT",
		"details": null
	}
}

```

## CLI上报 
### 安装CLI  
如何安装请参看<a href="https://docs.jdcloud.com/cn/cli/installation">安装说明</a> 。
### 配置环境  

配置KEY、所在区域region-id和网关地址endpoint，编辑 /root/.jdc/config
```
vi ~/.jdc/config
```

```
[default]
access_key = YourAccessKeyID
secret_key = YourAccessKeySecret
region_id = cn-north-1
endpoint = monitor.cn-north-1.jdcloud-api.com
scheme = https
timeout = 20
```  
不同地域的region_id 和 上报的网关endpoint地址如下：  

地域 |region_id |公网endpoint|内网endpoint
---|---|---|---
华北-北京 |cn-north-1| monitor.cn-north-1.jdcloud-api.com |monitor.internal.cn-north-1.jdcloud-api.com
华南-广州 |cn-south-1| monitor.cn-south-1.jdcloud-api.com |monitor.internal.cn-south-1.jdcloud-api.com
华东-宿迁 |cn-east-1 |monitor.cn-east-1.jdcloud-api.com  |monitor.internal.cn-east-1.jdcloud-api.com
华东-上海 |cn-east-2 | monitor.cn-east-2.jdcloud-api.com |monitor.internal.cn-east-2.jdcloud-api.com

### 上报监控数据  
使用 put-custom-metric-data 接口上报监控数据，示例如下：  
```
jdc monitor put-custom-metric-data --input-json '{"metricDataList": [{"namespace": "test_ns","metric": "vm.cpu.usage1","dimensions": {"host": "10.10.10.23","datacenter": "cn_north_1"},"timestamp": 1544425695,"type": 1,"values": {"value": "12342213"}}]}'
```  
注意：仅能上报近1周的监控数据，请将上边示例中timestamp 中的时间戳修改为你当前上报的UNIX时间。

返回成功示例如下：
```
{
    "error": null, 
    "result": {
        "errMetricDataList": [], 
        "success": true
    }, 
    "request_id": "bg9ofp78ikqqgvastas64owpqmoijk77"
}
```

 
