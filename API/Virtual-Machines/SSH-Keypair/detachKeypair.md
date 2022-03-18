# detachKeypair


## 描述

为云主机实例解绑密钥。

详细操作说明请参考帮助文档：[绑定密钥](https://docs.jdcloud.com/cn/virtual-machines/bind-keypair)

## 接口说明
- 实例已通过京东云绑定密钥，且实例须处于 **运行中** 或 **已停止** 状态。
- 解绑密钥后，须启动（停止状态绑定）或重启（运行状态绑定）实例才可生效。
- 密钥解绑功能依赖于镜像中内置的京东云官方系统组件，由于组件具备自动升级功能，因此通常情况下均支持密钥绑定功能。如需确认可进入系统运行`cat /usr/local/share/jcloud/agent/core/componentInfo.cfg`查看系统组件版本是否不低于`3.0.1042`。


## 请求方式
POST

## 请求地址
https://vm.jdcloud-api.com/v1/regions/{regionId}/keypairs/{keyName}:detach

|名称|类型|是否必需|示例值|描述|
|---|---|---|---|---|
|**regionId**|String|是|cn-north-1|地域ID。|
|**keyName**|String|是|test|密钥名称。|

## 请求参数
|名称|类型|是否必选|示例值|描述|
|---|---|---|---|---|
|**instanceIds**|String[]|是|\[&quot;i-eumm****d6&quot;,&quot;i-y5nh****9w&quot;]|要解绑的云主机实例ID列表。|


## 返回参数
|名称|类型|示例值|描述|
|---|---|---|---|
|**result**|[Result](detachKeypair#user-contemt-result)| |响应结果。|
|**requestId**|String|c2hmmaan8w06w19qcdfuic4w03f7ft2d|请求ID。|

### <div id="user-contemt-result">Result</div>
|名称|类型|示例值|描述|
|---|---|---|---|
|**successInstanceId**|String[]| |请求成功的云主机实例ID列表。|
|**failInstanceId**|String[]| |请求失败的云主机实例ID列表。|


## 请求示例
POST

```
/v1/regions/cn-north-1/keypairs/my-test:detach
{
    "instanceIds": ["i-eumm****d6", "i-y5nh****9w"]
}
```



## 返回示例
```
{
    "requestId": "e93c391d985886bba6c242270f4d91d8", 
    "result": {
        "failInstanceId": [
            "i-y5nh****9w"
        ], 
        "successInstanceId": [
            "i-eumm****d6"
        ]
    }
}
```

## 返回码
|HTTP状态码|错误码|描述|错误解析|
|---|---|---|---|
|**200**||OK||
|**400**|FAILED_PRECONDITION|Windows OS doesn't support attach keypair.|不支持操作windows实例。|
|**400**|FAILED_PRECONDITION|Invalid instance status xx|云主机状态异常。|
|**400**|FAILED_PRECONDITION|Already attached other keypair. instance id xx|该云主机没有绑定此密钥。|
|**404**|NOT_FOUND|Instance 'xx' not found.|云主机实例不存在。|
|**404**|NOT_FOUND|Keypair 'xx' not found|密钥不存在。|
|**500**|INTERNAL|Internal server error|系统内部错误，请稍后重试。如果多次尝试失败，请提交工单。|
|**500**|UNKNOWN|Unknown server error|服务暂时不可用，请稍后重试。如果多次尝试失败，请提交工单。|
