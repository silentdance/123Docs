# 功能介绍
**制作端通知云服务模型拼接完成**  

# URI
生产：https://webapi.123kanfang.com/v2/houseTask/FinishHouseTask  
测试：http://test.webapi.123kanfang.com:5000/v2/houseTask/FinishHouseTask


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
| packageId | No | String | 模型数据包的packageId |
| isFinished | No | bool | true：制作完成，false：无法制作 |

# 正确响应
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| state | No | Int | [返回状态](../Agreement/APIResponseState.md) | 
| payload | No | Object | 返回的数据载体 |
| payload.id | No | string(32) | 任务ID，当任务状态为非完结时，同一个customerHouseId对应的任务ID是恒定的。 |
| payload.taskState | No | Int | [任务状态](../Agreement/TaskState.md) |


## Schema
```json
	{
	    "state": 200,
	    "payload": {
	        "id": "707fc88e14d34076b827df8fd758887b",
	        "taskState": 50000,
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