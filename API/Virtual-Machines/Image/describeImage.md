# describeImage


## 描述

查询镜像详情。

详细操作说明请参考帮助文档：[镜像概述](https://docs.jdcloud.com/cn/virtual-machines/image-overview)

## 接口说明
- 该接口与查询镜像信息列表返回的镜像信息一致。
- 只需要查询单个镜像信息的时候可以调用该接口。


## 请求方式
GET

## 请求地址
https://vm.jdcloud-api.com/v1/regions/{regionId}/images/{imageId}

|名称|类型|是否必需|示例值|描述|
|---|---|---|---|---|
|**regionId**|String|是|cn-north-1|地域ID。|
|**imageId**|String|是|i-eumm****d6|镜像ID。|

## 请求参数
无


## 返回参数
|名称|类型|示例值|描述|
|---|---|---|---|
|**result**|[Result](describeImage#user-content-result)| |响应结果。|
|**requestId**|String|c2hmmaan8w06w19qcdfuic4w03f7ft2d|请求ID。|

### <div id="user-content-result">Result</div>
|名称|类型|示例值|描述|
|---|---|---|---|
|**image**|[Image](describeImage#user-content-image)| |镜像信息。|

### <div id="user-content-image">Image</div>
|名称|类型|示例值|描述|
|---|---|---|---|
|**imageId**|String|img-m5s0****29|镜像ID。|
|**name**|String|image-test |镜像名称。|
|**platform**|String|CentOS|镜像的操作系统平台名称。<br>可能值：`Ubuntu、CentOS、Windows Server、Other Linux、Other Windows`。<br>|
|**osVersion**|String|8.2|镜像的操作系统版本。|
|**architecture**|String|x86_64|镜像架构。可能值：`x86_64、i386`。|
|**systemDiskSizeGB**|Integer|40|镜像系统盘大小。|
|**imageSource**|String|public|镜像来源，可能值：<br>`public`：官方镜像。<br>`thirdparty`：镜像市场镜像。<br>`private`：用户自己的私有镜像。<br>`shared`：其他用户共享的镜像。<br>`community`：社区镜像。<br>|
|**osType**|String|linux|镜像的操作系统类型。可能值：`windows、linux`。|
|**status**|String|ready|镜像状态。参考 [镜像状态](https://docs.jdcloud.com/virtual-machines/api/image_status)。|
|**createTime**|String|2020-08-21 11:36:36|镜像的创建时间。|
|**sizeMB**|Integer|3244|镜像文件的实际大小。|
|**desc**|String| |镜像描述。|
|**ownerPin**|String| |该镜像拥有者的用户PIN。|
|**launchPermission**|String|all|镜像的使用权限。可能值：<br>`all`：所有人均可使用（官方镜像和镜像市场镜像会返回此值）。<br>`specifiedUsers`：镜像存在共享关系，仅拥有者和共享对象可以使用。<br>`ownerOnly`：镜像不存在共享关系，仅拥有者可以使用。<br>|
|**systemDisk**|[InstanceDiskAttachment](describeImage#user-content-instancediskattachment)| |镜像系统盘配置。|
|**dataDisks**|[InstanceDiskAttachment[]](describeImage#user-content-instancediskattachment)| |镜像数据盘配置列表。|
|**snapshotId**|String|snapshot-h8u1****36|创建云盘系统盘所使用的快照ID。系统盘类型为本地盘的镜像，此参数为空。|
|**rootDeviceType**|String|cloudDisk|镜像支持的系统盘类型。可能值：<br>`localDisk`：本地盘系统盘。<br>`cloudDisk`：云硬盘系统盘。<br>|
|**progress**|String|100|镜像复制和镜像类型转换时的进度，仅显示数值，单位为百分比。|
|**offline**|Boolean| |镜像的上下线状态。仅官方镜像和云市场镜像返回此值。<br>可能值：`true` ：已下线；`false`：未下线。|


### <div id="user-content-instancediskattachment">InstanceDiskAttachment</div>
|名称|类型|示例值|描述|
|---|---|---|---|
|**diskCategory**|String|cloud|磁盘类型。可能值：<br>**系统盘**：`local` ：本地盘；`cloud` ：云硬盘。<br>**数据盘**：`cloud`：云硬盘。<br>|
|**autoDelete**|Boolean|true|是否随实例一起删除，即删除实例时是否自动删除此磁盘。此参数仅对按配置计费的非多点挂载云硬盘生效。可能值：<br>`true`：随实例删除。<br>`false`：不随实例删除。<br>|
|**localDisk**|[LocalDisk](describeImage#user-content-localdisk)| |仅本地系统盘返回此参数。对应 `diskCategory=local`。|
|**cloudDisk**|[Disk](describeImage#user-content-clouddisk)| |云硬盘配置。对应 `diskCategory=cloud`。|
|**deviceName**|String|vdb|磁盘逻辑挂载点。<br>**系统盘**：默认为vda。<br>**数据盘**：返回值：`[vdb~vdbm]`。<br>|


### <div id="user-content-localdisk">LocalDisk</div>
|名称|类型|示例值|描述|
|---|---|---|---|
|**diskType**|String||本地系统盘镜像不返回此参数。|
|**diskSizeGB**|Integer|120|磁盘容量。单位为 GiB。|

### <div id="user-content-clouddisk">Disk</div>
|名称|类型|示例值|描述|
|---|---|---|---|
|**diskType**|String| ssd.gp1|云硬盘类型。可能值： `ssd.gp1,ssd.io1,hdd.std1`|
|**diskSizeGB**|Integer| |云硬盘容量，单位为 GiB。|
|**iops**|Integer| |该云硬盘实际应用的iops值。|
|**snapshotId**|String| |创建该云硬盘的快照ID。|
|**encrypted**|Boolean| |制作快照的磁盘是否为加密盘。|

## 请求示例
GET

```
/v1/regions/cn-north-1/images/img-m5s0****29
```



## 返回示例
```
{
    "requestId": "0d1531eb5016b64d801a9e24bac779e8", 
    "result": {
        "image": {
            "architecture": "x86_64", 
            "createTime": "2021-01-28 16:49:05", 
            "desc": "", 
            "imageId": "img-m5s0****29", 
            "imageSource": "public", 
            "launchPermission": "all", 
            "name": "CentOS 8.2 64位", 
            "osType": "linux", 
            "osVersion": "8.2", 
            "ownerPin": "admin", 
            "platform": "CentOS", 
            "progress": "100", 
            "rootDeviceType": "cloudDisk", 
            "sizeMB": 2494, 
            "snapshotId": "snapshot-h8u1****36", 
            "status": "ready", 
            "systemDisk": {
                "autoDelete": true, 
                "cloudDisk": {
                    "diskSizeGB": 40, 
                    "diskType": "ssd.gp1", 
                    "encrypt": false, 
                    "encrypted": false, 
                    "snapshotId": "snapshot-h8u1****36"
                }, 
                "deviceName": "vda", 
                "diskCategory": "cloud"
            }, 
            "systemDiskSizeGB": 40, 
            "uefiSupport": false
        }
    }
}
```

## 返回码
|HTTP状态码|错误码|描述|错误解析|
|---|---|---|---|
|**200**||OK||
|**404**|NOT_FOUND|Image 'xx' not found|镜像不存在。|
|**500**|INTERNAL|Internal server error|系统内部错误，请稍后重试。如果多次尝试失败，请提交工单。|
|**500**|UNKNOWN|Unknown server error|服务暂时不可用，请稍后重试。如果多次尝试失败，请提交工单。|
