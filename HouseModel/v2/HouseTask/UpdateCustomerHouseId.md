# 功能介绍
**更新数据包上绑定的客户房源ID**  

# URI
生产：https://webapi.123kanfang.com/v2/houseTask/UpdateCustomerHouseId  
测试：https://webapi-test.123kanfang.com/v2/houseTask/UpdateCustomerHouseId


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
| packageId | Yes | String | 模型数据包的packageId, 注意！与houseTaskId互斥，如果两个参数都传了，会优先使用HouseTaskId。 |
| houseTaskId | Yes | String | 模型数据包的主键Id，注意！与packageId互斥，如果两个参数都传了，会优先使用HouseTaskId。 |

# 正确响应
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| state | No | Int | [返回状态](../Agreement/APIResponseState.md) | 
| payload | No | Object | 返回数据的载体 |
| payload.packageId | No | String | 数据包ID |
| paylaod.customerHouseId | No | String | 客户房源ID |


## Schema
```json
{
    "state": 200,
    "payload": {
      "packageId": "<PackageId>",
      "customerHouseId" : "<CustomerHouseId>"
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
