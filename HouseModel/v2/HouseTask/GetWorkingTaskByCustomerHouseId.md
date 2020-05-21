# 功能介绍
**根据客户房源ID查询未完结的3d看房任务**  
注：此接口目前用来前置在 【创建拍摄任务】之前，用来检测某个客户ID是否可以创建拍摄任务，在其他相同ID的任务完成前，不允许创建拍摄任务。  

# URI
生产：https://webapi.123kanfang.com/v2/houseTask/GetWorkingTaskByCustomerHouseId  
测试：http://test.webapi.123kanfang.com:5000/v2/houseTask/GetWorkingTaskByCustomerHouseId

# Method
**Post with Form**

# 身份认证
| 位置| 参数名 | 可空 | 参数类型 | 描述 |
| ------ | ------ | ------ | ------ | ------ |
| Header | Authorization | Yes | String | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。|
| Query | Authorization | Yes | String | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。|
| Cookie | Authorization | Yes | String | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。|


# 请求头
| 参数 | 可空 | 参数类型 | 描述 |
| ---- | ---- | ---- | ----|
| Content-Type | No | String | 值应为：application/x-www-form-urlencoded |
| Authorization | Yes | String | 身份认证的Token, 在身份认证表中任意位置传输均可。| 


# 请求参数
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| customerHouseId | No | String(64) | 客户的房源ID  |

# 正确响应
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| state | No | Int | [返回状态](../Agreement/APIResponseState.md) | 
| payload | No | Object | 返回的数据载体 |
| payload[x] | No | Array | 未完结的任务列表 |
| payload[x].customerHouseId| No | String | 客户的房源ID |
| Payload[x].packageId | No | String | 数据包ID，当任务状态为非完结时，同一个customerHouseId对应的PackageId是恒定的。 |
| payload[x].taskState | No | String | [任务状态](../Agreement/TaskState.md) |


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