功能介绍
========

获取身份授权的Token

 

URI
===
正式环境：  
https://webapi.123kanfang.com/v2/Authorization/GetAccessToken  
测试环境：  
http://webapi-test.123kanfang.com/v2/Authorization/GetAccessToken
 

Method
======

GET

 

身份认证
========
无

 

请求头
======
无

请求参数
========

| 参数  | 可空 | 参数类型 | 描述     |
|-----------|----------|--------------|--------------|
| authKey   | No       | String       | 登录的用户名 |
| authValue | No       | String       | 登录的密码   |
| clientEdtion | Yes   | String       | 登录客户端的来源， 如果该已经配置的版本的登录限制，需要传特定的值以验证版本，如果是客户方服务器调用，可以传固定值ps_1.0.0, 即partner server 版本 1.0.0 |

正确响应
========

| 字段名                   | 可空 | 数据类型 | 描述  |
|-------|----------|------|-----|
| state                        | No       | Int          | [返回状态](../Agreement/APIResponseState.md) |
| payload                      | No       | Object       | 返回的数据载体 |
| payload.token                | No       | String       | 返回的AccessToken |
| payload.tokenExpireIn        | No       | Int          | token的寿命，以秒为单位。|
| payload.refreshToken         | No       | String       | 返回的RefreshToken  |
| payload.refreshTokenExpireIn | No       | Int          | RefreshToken的寿命，以秒为单位。|

示例
``` json
{
    "state": 200,
    "payload": {
        "token": "<access token",
        "tokenExpireIn": 172800,
        "refreshToken": "<refreshToken",
        "refreshTokenExpireIn": 2592000
    }
}
```
 
错误响应
========

| 字段名 | 可空 | 数据类型 | 描述  |
|------------|----------|--------------|-------|
| state      | No       | Int          | [返回状态](../Agreement/APIResponseState.md) |
| payload    | No       | String       | 错误信息 |

示例
``` json
 {
    "state": 401,
    "payload": "error detail"
 }
```
