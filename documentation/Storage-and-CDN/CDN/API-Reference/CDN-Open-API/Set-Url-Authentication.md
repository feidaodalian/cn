# **设置URL鉴权**

## **1. 描述**

仅中国境内加速域名可配置。设置url鉴权 (setAccessKeyConfig)

## **2. 请求参数**

| **名称**   | **类型** | **是否必填** | **描述**                                                     |
| ---------- | -------- | ------------ | ------------------------------------------------------------ |
| username   | String   | 是           | 京东用户名pin                                                |
| signature  | String   | 是           | 用户签名，通过md5的方式校验用户的身份信息，保障信息安全。</br>md5=日期+username+秘钥SecretKey; 日期：格式为 yyyymmdd; username：京东用户名pin; 秘钥：双方约定; </br>示例：比如当前日期2016-10-23,用户pin:jcloud_00,用户秘钥SecretKey：e7a31b1c5ea0efa9aa2f29c6559f7d61,那签名为MD5(20161023jcloud_00e7a31b1c5ea0efa9aa2f29c6559f7d61)  |
| domain     | String   | 是           | 加速域名     |
| accesskeyType | String   | 是           |鉴权类型，0表示无鉴权，1表示参数鉴权，2表示路径鉴权 |
| accesskeyKey | String   | 是           | 密码，长度为8到32 |
|accesskeyKeep | String   | 是           |是否是回源鉴权 0表示是 1表示否 |

## **3. 返回参数**

| **名称** | **描述**                                                  |
| -------- | --------------------------------------------------------- |
| status   | 结果状态，表示接口请求成功与否，成功用0表示，其他表示失败 |
| msg      | 提示信息                                                  |
| data     | 返回数据                                                  |

## **4. 调用示例**

- ### **请求地址**

https://opencdn.jcloud.com/api/setAccessKeyConfig

- ### **请求示例**

 https://opencdn.jcloud.com/api/setAccessKeyConfig

* json格式

```
{
    "username" :"test_user",
    "signature" :"d00f58f89e8cd55dc080aec0d8051845",
    "domain" :"www.a.com",
    "accesskeyType" :"0",
    "accesskeyKey" :"526f20b2921957b",
    "accesskeyKeep" :"1"
 }
```

- ### **返回示例**

* json格式

```
{
  "status": 0,
  "msg": "成功",
  "data": "test1.dev.opencdn.jcloud.com"
}

```

 
