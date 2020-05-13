# 功能介绍

**服务器通用通知转发接口**

# URI

生产：https://im.123kanfang.com/IM/Notify

测试：https://im-test.123kanfang.com/IM/Notify


# Method

**Post with Form**


# 身份认证

[加固接口的签名验证](../Agreement/StongValidation.md)


# 请求头

| 参数                               | 可空 | 参数类型 | 描述                  |
| ---------------------------------- | ---- | -------- | --------------------- |
| Content-Type                       | No   | String   | x-www-form-urlencoded |
| 剩余的字段按照客户的需求变化而变化 |      |          |                       |


# 请求参数

| 字段名                             | 可空 | 参数类型 | 描述           |
| ---------------------------------- | ---- | -------- | -------------- |
| app                                | No   | String   | 123AppKey      |
| action                             | No   | String   | 约束的转发行为 |
| 剩余的字段按照客户的需求变化而变化 |      |          |                |


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
