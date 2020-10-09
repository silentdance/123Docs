# 功能介绍
**请求房源数据包推送，可推送安居客，客户自有ERP等**

# URI
生产：https://webapi.123kanfang.com/v2/houseTask/AddNewNotifyTaskByPackageID  
测试：http://test.webapi.123kanfang.com:5000/v2/houseTask/AddNewNotifyTaskByPackageID


# Method
**Post with Form**


# 身份认证
| 位置| 参数名 | 可空 | 参数类型 | 描述 |
| ------ | ------ | ------ | ------ | ------ |
| Header | Authorization | Yes | String | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。|
| FormBody [x-www-form-urlencoded] | Authorization | Yes | String | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。|
| Cookie | Authorization | Yes | String | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。|


# 请求头
| 参数 | 可空 | 参数类型 | 描述 |
| ---- | ---- | ---- | ----|
| Content-Type | No | String | 值应为：application/x-www-form-urlencoded |
| Authorization | Yes | String | 身份认证的Token, 在身份认证表中任意位置传输均可。| 


# 请求参数
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| packageId | No | String(128) | 数据包ID |
| notifyconfigId | No | String(32) | 配置ID （联系123获取该ID） |
| forcePush | Yes | Bool | 123默认不会进行二次推送，如果需要二次推送，设置此值为True来强制推送，注意：此参数仅仅用来需要重推数据包的场景使用，在不需要推送的场景频繁的应用此参数会被封掉推送能力。 |
| payload | Yes | String(255) | 新建推送任务的额外数据，通常用来满足客户的特殊需求，一般是一个Json格式。 |

# 正确响应
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| state | No | Int | [返回状态](../Agreement/APIResponseState.md) | 
| payload | No | Object | 返回的数据载体 |
| payload.id | No | string | 推送任务ID |
| payload.notifyResult | No | Int | [通知状态](../Agreement/NotifyResult.md) |
| payload.notifyConfigId | No | string | 通知配置ID |
| payload.houseTaskId | No | string | 房源任务ID |


## Schema
```json
{
    "state": 200,
    "payload":  {
        "id": "3lNlZHxVEku1HoT1qdrAng",
        "state": 0
    }
}
```

# 错误相应
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| state | No | Int | [返回状态](../Agreement/APIResponseState.md) | 
| state | No | String | 错误代码或Message | 

## Schema 
``` json
{
    "state": 401,
    "payload": "Unauthorized"
}
```

``` json
{
    "state": 403,
    "payload": "InvalidXXXXXX"
}
```

``` json
{
    "state": 500,
    "payload": "InnerServerError -> detail xxxxxx"
}
```
