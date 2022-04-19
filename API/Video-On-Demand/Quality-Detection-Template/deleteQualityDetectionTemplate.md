# deleteQualityDetectionTemplate


## 描述
删除质检模板

## 请求方式
DELETE

## 请求地址
https://vod.jdcloud-api.com/v1/qualityDetectionTemplates/{templateId}

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**templateId**|Long|True| |模板ID|

## 请求参数
无


## 返回参数
|名称|类型|描述|
|---|---|---|
|**requestId**|String|请求ID|


## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
|**400**|Invalid parameter|
|**401**|Authentication failed|
|**404**|Not found|
|**500**|Internal server error|
|**503**|Service unavailable|

## 请求示例
DELETE
```
https://vod.jdcloud-api.com/v1/qualityDetectionTemplates/1

```
