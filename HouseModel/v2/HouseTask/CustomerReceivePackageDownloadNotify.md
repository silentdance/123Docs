# 功能介绍
**客户自有ERP接受推送消息，再根据推送消息去下载数据包**

注： 此操作需要做成异步操作，即接到消息之后往消息队列或者数据库放一套消息，后端再有其他程序去下载数据包（可以有失败重试）。


# URI
**由客户方提供**


# Method
**Post with Form**


# 身份认证
[加固接口的签名验证](../Agreement/StrongValidation.md)


# 请求头
| 参数 | 可空 | 参数类型 | 描述 |
| ---- | ---- | ---- | ----|
| Content-Type | No | String | x-www-form-urlencoded |
| sign | Yes | String | 根据[加固接口的签名验证](../Agreement/StrongValidation.md)规则生成出来的签名。| 


# 请求参数
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| state | No | String(128) | 制作任务的最终制作状态，（Finished，Cancel，Failed）|
| panoramaPackage | Yes | String (4000) | 若制作成功此列为客户获取数据包的途径，参考客户下载123数据包的方式, **注意！一定不要用下载链接中的文件名作为转存的包的名字，123推送的下载地址文件名有可能会跟PackageId不一致。切记！切记！切记！** | 
| fileHash | No | String(32) | 当下载方式为Zip时，值为数据包的MD5 Hash校验码，否则无此参数 | 
| houseId | No | String(64) | 客户方的房源ID | 
| packageId | No | String(128) | 数据包的ID |
| cityId | Yes |String (32) | 城市ID，值为客户内网的城市ID的值 | 
| notifyId | No | string(22) | 123内部的当次通知任务的ID | 
| comments | Yes | String(255) | 目前用来存放制作失败时的失败原因 |  

**还可以通过配置添加其他参数，只要房源任务有该数据，就可以通过配置实现推送给客户方，参数名由客户方指定** 


# 正确响应
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| state | No | Int | [返回状态](../Agreement/APIResponseState.md) | 
| payload | No | String | 客户方想返回的msg，如果没有可为空 |

## Schema
```json
{
    "state": 200,
    "payload":  "Success"
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
