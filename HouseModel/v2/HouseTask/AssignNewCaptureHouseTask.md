# 功能介绍
**第三方企业客户为旗下摄影师指派拍摄任务。**

# URI
生产：https://webapi.123kanfang.com/v2/houseTask/AssignNewCaptureHouseTask  
测试：http://test.webapi.123kanfang.com:5000/v2/houseTask/AssignNewCaptureHouseTask


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
| userName | No | String(32) | 摄影师在客户组织内的唯一标识，可以是员工号，手机号，邮箱等，123会自动生成该摄影师的账号，在123生成的用户名规则为：组织代码 + 摄影师账户名，初始密码为123456  |
| houseName | No | String(128) | 房源名 |
| customerHouseId | No | String(64) | 客户的房源ID |
| serviceId | No | String(32) | 客户的服务ID |
| additionalData | No | String(1024) | 房源名 |
| cityId | No | String(32) | 城市ID |
| houseType | No | String(32) | 房源类型 |
| layout | No | String(64) | 户型信息，x室x厅x卫 |

# 正确响应
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| state | No | Int | [返回状态](../Agreement/APIResponseState.md) | 
| payload | No | Object | 返回的数据载体 |
| payload.id | No | string(32) | 任务ID，当任务状态为非完结时，同一个customerHouseId对应的任务ID是恒定的。 |
| payload.userId | No | string(32) | 当前摄影师在123系统内的ID |
| payload.customerHouseId | No | string(64) | 客户的房源ID |
| payload.packageId | No | string(128) | 数据包ID，当任务状态为非完结时，同一个customerHouseId对应的PackageId是恒定的。 |
| payload.serviceId | No | Int | 客户的服务ID |
| payload.taskState | No | Int | [任务状态](../Agreement/TaskState.md) |



## Schema
```json
{
    "state": 200,
    "payload": {
        "id": "707fc88e14d34076b827df8fd758887b",
        "userId": "e3e0bc34c03c4253a0dab2faebc7adee",
        "customerHouseId": "HN1137521",
        "houseId": "sushiming@tujia.com_1f16721ab10e4c24aa36f220ee4cff19",
        "productId": "5c0e3064216c4affaf7ef2aa00683d27",
        "taskState": 10000,
        "houseName": "少女心粉色ins大学城淹城春秋乐园动物园"
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