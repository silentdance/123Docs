功能介绍
========

刷新身份授权的Token

URI
===
正式环境：  
https://webapi.123kanfang.com/v2/Authorization/RefreshToken
测试环境：  
http://webapi.123kanfang.com:5000/v2/Authorization/RefreshToken

Method
======

GET

身份认证
========

| 位置 | 参数名    | 可空 | 参数类型 | 描述                                                        |
|----------|---------------|----------|--------------|-----|
| Header   | Authorization | Yes      | String       | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。 |
| Query    | Authorization | Yes      | String       | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。 |
| Cookie   | Authorization | Yes      | String       | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。 |

请求头
======

| 参数      | 可空 | 参数类型 | 描述                                          |
|---------------|----------|--------------|---------------------------------------------------|
| Authorization | Yes      | String       | 身份认证的Token, 在身份认证表中任意位置传输均可。 |

请求参数
========

| 参数  | 可空 | 参数类型 | 描述     |
|-----------|----------|--------------|--------------|
| authKey   | No       | String       | 登录的用户名 |
| authValue | No       | String       | 登录的密码   |

正确响应
========

| 字段名                   | 可空 | 数据类型 | 描述  |
|------------------------------|----------|--------------|-----|
| state                        | No       | Int          | [返回状态](../Agreement/APIResponseState.md) |
| payload                      | No       | Object       | 返回的数据载体 |
| payload.token                | No       | String       | 返回的AccessToken |
| payload.tokenExpireIn        | No       | Int          | token的寿命，以秒为单位。 |
| payload.refreshToken         | No       | String       | 返回的RefreshToken  |
| payload.refreshTokenExpireIn | No       | Int          | RefreshToken的寿命，以秒为单位。|

示例
``` json
 {
    "state": 200,
    "payload": {
        "token": "access token",
        "tokenExpireIn": 172800,
        "refreshToken": "refreshToken",
        "refreshTokenExpireIn": 2592000
    }
 }
```

错误响应
========

| 字段名 | 可空 | 数据类型 | 描述 |
|------------|----------|--------------|-------|
| state      | No       | Int          | [返回状态](../Agreement/APIResponseState.md) |
| payload    | No       | String       | 错误信息 |

示例
``` json
{
   "state": 4011,
   "payload": "error detail"
}
```