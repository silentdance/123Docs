# 功能介绍
**B端客户同步客户系统内的账户至123看房，注意此接口必须是组织账号才能调用，创建用户的规则是 组织代码-用户名**
 

# URI
生产：https://webapi.123kanfang.com/v2/user/CreateSubAccount  
测试：https://webapi-test.123kanfang.com:5000/v2/user/CreateSubAccount
 
# Method
**Post with form**

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
========

| 参数        | 可空 | 参数类型   | 描述             |
|-------------|------|------------|------------------|
| subAccount  | Yes   | String(64) | 账户名    |
| parentAccount  | Yes   | String(64) | 房源数据包ID    |
| accountType | Yes | String(16) |账户类型（Group 组；Admin 管理员；Staff 制作人）默认是Staff|

# 正确响应
========

| 字段名 | 可空 | 数据类型 | 描述  |
|------------           |----------|--------------  |----------|
| state                 | No       | Int            | [返回状态](../Agreement/APIResponseState.md) |
| payload               | No       | Object         | OK |
| payload.userId        | No       | String(32)     | 用户ID |
| payload.userName      | No       | String(32)     | 账户名，实际创建的账户名会是 组织代码-账户名的格式，例如：组织代码是 TG，传入的subAccount参数是TestAccount, 则实际的用户名是 TG-TestAccount. |
| payload.regionName    | No       | String(32)     | 区域名 |
| payload.parentId      | No       | String(32)     | 父账户ID |
| payload.createTime    | No       | String(32)     | 创建时间 |

 
# 示例

``` json
{
    "state": 200,
    "payload": "OK"
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
