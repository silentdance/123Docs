# 功能介绍

**客户提供接口，接收用户同意提供电话的消息**

该接口会在用户同意给出电话后由123后台调用  
注：该接口是客户方已经有看房用户的电话，仅仅是授权给经济人的接口调用方式，一般是应用于中大型的看房中介行业。  

# URI

**由客户方提供**


# Method

**Post with Form**


# 身份认证

[加固接口的签名验证](../Agreement/StrongValidation.md)


# 请求头

| 参数         | 可空 | 参数类型 | 描述                                                         |
| ------------ | ---- | -------- | ------------------------------------------------------------ |
| Content-Type | No   | String   | x-www-form-urlencoded                                        |
| sign         | Yes  | String   | 根据[加固接口的签名验证](../Agreement/StongValidation.md)规则生成出来的签名。 |


# 请求参数

| 字段名     | 可空 | 数据类型    | 描述             |
| ---------- | ---- | ----------- | ---------------- |
| packageId  | No   | string(128) | 数据包id         |
| meetingId  | No   | int         | 123定义的会议id  |
| agreeTime  | No   | DateTime    | 同意给电话的时间 |
| customerId | No   | string(32)  | 用户Id           |
| agentId    | No   | string(32)  | 客户Id           |


# 正确响应

| 字段名  | 可空 | 数据类型 | 描述                                         |
| ------- | ---- | -------- | -------------------------------------------- |
| state   | No   | Int      | [返回状态](../Agreement/APIResponseState.md) |
| payload | No   | String   | 客户方想返回的msg，如果没有可为空            |

## Schema

```json
{
    "state": 200,
    "payload":  "Success"
}
```

# 错误响应

| 字段名  | 可空 | 数据类型 | 描述                                         |
| ------- | ---- | -------- | -------------------------------------------- |
| state   | No   | Int      | [返回状态](../Agreement/APIResponseState.md) |
| payload | No   | String   | 错误代码或Message                            |

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
