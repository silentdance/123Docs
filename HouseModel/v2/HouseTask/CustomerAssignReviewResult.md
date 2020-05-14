# 功能介绍
**客户审核已做完的房子**  

# URI
生产：https://webapi.123kanfang.com/v2/houseTask/CustomerAssignReviewResult  
测试：http://test.webapi.123kanfang.com:5000/v2/houseTask/CustomerAssignReviewResult


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
| reviewResult | No | int | 0：通过，1：重新制作，2：取消制作，3：无法制作需要补拍 |
| comments | Yes | String(128) | 备注 |

# 正确响应
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| state | No | Int | [返回状态](../Agreement/APIResponseState.md) | 
| payload | No | Object | 返回的数据载体 |
| payload.packageId | No | string(128) | 数据包ID，当任务状态为非完结时，同一个customerHouseId对应的PackageId是恒定的。 |
| payload.taskState | No | Int | [任务状态](../Agreement/TaskState.md) |


## Schema
```json
	{
	    "state": 200,
	    "payload": {
	        "houseId": "sushiming@tujia.com_1f16721ab10e4c24aa36f220ee4cff19",
	        "productId": "5c0e3064216c4affaf7ef2aa00683d27",
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