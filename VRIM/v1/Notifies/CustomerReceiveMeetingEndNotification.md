# 功能介绍

**客户提供接口接收带看结束的推送，以记录带看的会议信息**

该接口会在会议结束（主动或被动）后被123后台调用，以推送相关信息给客户的后台


# URI

**由客户方提供**


# Method

**Post with Form**


# 身份认证

[加固接口的签名验证](../Agreement/StongValidation.md)


# 请求头

| 参数         | 可空 | 参数类型 | 描述                                                         |
| ------------ | ---- | -------- | ------------------------------------------------------------ |
| Content-Type | No   | String   | x-www-form-urlencoded                                        |
| sign         | Yes  | String   | 根据[加固接口的签名验证](../Agreement/StongValidation.md)规则生成出来的签名。 |

# 请求参数

| 字段名    | 可空 | 数据类型    | 描述                             |
| --------- | ---- | ----------- | -------------------------------- |
| packageId | No   | string(128) | 数据包id                         |
| meetingId | No   | int         | 123定义的会议id                  |
| endTime   | No   | DateTime    | 结束时间                         |
| users     | No   | string(max) | 与会的所有人的用户ID，用逗号隔开 |


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
| message | No   | String   | 错误代码或Message                            |

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