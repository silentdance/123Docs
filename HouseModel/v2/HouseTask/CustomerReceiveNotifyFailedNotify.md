# 功能介绍
**数据包推送是一个比较复杂的过程，中间是有概率失败的，此接口用来通知客户通知过程中发生了异常**

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


# 请求参数
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| notifyId | No | String(32) | 当前推送的推送任务ID |
| notifyConfigId | No | String(32) | 当此推送使用的推送配置ID | 
| notifyType | No | String(32) | 通知类型 | 
| notifyResult | No | Enum(int) | 当前的通知结果,0： 未推送，1：推送成功，2，推送失败（客户方拒绝请求），3:推送异常（因数据或程序导致推送异常） | 
| param | Yes | string(22) | 如果是在网络请求后接通后，客户方服务器发生了异常，此时会记录请求参数。 | 
| response | Yes | String(1024) | 用来存放失败的具体原因 |  
| cityId | Yes | String(32) | 当前房源的城市ID，如果有的话 | 
| packageId | No | String(64) | 数据包ID | 
| houseId | Yes | String(32) | 客户方房源ID | 
| state | Yes | int | 房源状态的枚举 | 

注：还可以根据客户方需要配置额外的参数，需要跟123开发进行对接。


# 响应
目前仅仅做抄送通知，不做任何记录，当发生网络异常时，该通知会自动重试三次。
