# 功能介绍
**获取房源列表**

# URI
生产：https://webapi.123kanfang.com/v2/houseTask/GetPage  
测试：http://test.webapi.123kanfang.com:5000/v2/houseTask/GetPage


# Method
**GET**


# 身份认证
| 位置| 参数名 | 可空 | 参数类型 | 描述 |
| ------ | ------ | ------ | ------ | ------ |
| Header | Authorization | Yes | String | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。|
| Query | Authorization | Yes | String | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。|
| Cookie | Authorization | Yes | String | 身份认证的Token，列表中任选一个位置传递此参数，此参数为必填项。|


# 请求头
| 参数 | 可空 | 参数类型 | 描述 |
| ---- | ---- | ---- | ----|
| Authorization | Yes | String | 身份认证的Token, 在身份认证表中任意位置传输均可。| 


# 请求参数
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| userName | Yes | String(32) | 摄影师的用户名（模糊匹配） |
| houseName | Yes | String(32) | 房源名（模糊匹配） |
| customerHouseId | Yes | String(32) | 客户房源ID（精确匹配） |
| searchKey | Yes | String(32) | 按模糊搜索的方式匹配客户房源ID或房源名 |
| userId | Yes | String(32) | 摄影师ID（精确匹配） |
| billOwnerId | Yes | String(32) | 账单人ID（精确匹配） |
| serviceId | Yes | String(32) | 服务ID（精确匹配） |
| packageId | Yes | String(64) | 数据包的ID，可以填写多个，多个可以使用同一个key不同的值，例如packageId=xxxxxx&packageId=xxxxxxx | 
| exceptPackageIds | Yes | String | 需要排除出结果集之外数据包的ID，可以填写多个，多个可以使用同一个key不同的值，例如exceptPackageIds=xxxxxx&exceptPackageIds=xxxxxxx | 
| commaSeparatedExceptPackageIds | Yes | String | 需要排除出结果集之外数据包的ID，与exceptPackageIds功能一致,主要是满足一些编程语言网络框架的限制，优先级比exceptPackageIds要低，可以填写多个(不能超过50个)，多个值之间用,分割。 | 
| status | Yes | Int | 房源的状态，可以填写多个，多个可以使用同一个key不同的值，例如status=0&status=10000 |
| stateStart | Yes | Int | 和stateEnd配合使用，限定查询任务的状态的最小值 |
| stateEnd | Yes | Int | 和stateStart配合使用, 限定查询任务的状态的最大值 |
| showNotifyType | Yes | String(32) | 指定通知结果的类型（推自己，推家装，推平台等，默认是推自己），只有Field中指定了NotifyResult后该参数才会生效。 |
| NotifyResult | Yes | Int | 按推送结果筛选数据（会结合showNotifyType匹配推送结果），只有Field中指定了NotifyResult后该参数才会生效。不传：不做筛选，-1：未创建拍摄任务，-0：等待推送，1：推送成功，2：推送失败，3：推送异常 |
| createStart | Yes | DateTime | 和endDate配合使用，限定任务创建时间的最小值 |
| createEnd | Yes | DateTime | 和startData配合使用, 限定任务创建时间的最大值 |
| modifyStart | Yes | DateTime | 和modifyEndDate配合使用，限定任务修改时间的最大值 |
| modifyEnd | Yes | DateTime | 和modifyStartDate配合使用，限定任务修改时间的最小值 |
| taskDemand | Yes | bool | 是否需要查询TaskDemand |
| path | Yes | String(64) | 根据userPath查询用户的房源数据，使用startwith规则匹配 |
| fields | Yes | String(256) | 可以根据 [需要的字段](#Fields) 选择想要的字段，每个字段用,分割 |
| mappingToUserKey | Yes | bool | cityId,houseType是否需要映射为客户方的，默认是不需要映射 |
| orderBy | Yes | String(32) | 排序的依据字段 |
| page | Yes | int | 页码，默认值为0 |
| pageSize | Yes | int | 分页尺寸，默认值为10 |


## SELECT Fields
<a id="Fields"></a>
* Id (默认)
* PackageId (默认)
* UserId (默认)
* HouseName (默认)
* CustomerHouseId (默认)
* CreateTime (默认)
* CaptureTime (默认)
* UploadTime (默认)
* TaskState (默认)
* UserComments (默认)
* Floors (默认)
* Rooms (默认)
* Points (默认)
* Bucket (默认)
* BillOwnerId
* Path
* ServiceId
* AdditionalData
* LastModifyTime
* Area
* HouseLayout
* LockedBy
* LockUntil
* LastHistoryId
* CityId
* HouseType
* PackageVersion
* Domain
* Comments (低性能)
* NotifyResult (低性能)
* UserName (低性能)

注意！标注为低性能的会导致连表查询，会降低查询性能。  
注意！一旦选择Fields所有默认Field将失效，需要手动指定选择的列。

## Order By
* CreateTime DESC | CreateTime ASC
* UploadTime DESC | UploadTime ASC
* LastModifyTime DESC | LastModifyTime ASC

# 正确响应tod
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| state | No | Int | [返回状态](../Agreement/APIResponseState.md) | 
| payload | No | Object | 返回的数据载体 |
| payload.total | No | int | 总数据条数 |
| payload.rows | No | Array | 当前分页的数据 |
| **注意！以下返回值会根据Fields参数的不同而不同** |
| payload.rows[x].additionalData| Yes | String(255) | 额外的数据可以存放在这里，一般以json的方式存储 |
| payload.rows[x].area| Yes | String(255) | 房源面积 |
| payload.rows[x].billOwnerId| Yes | String(255) | 账单人ID |
| payload.rows[x].bucket| Yes | String(255) | 目标存储介质的桶 |
| payload.rows[x].cityId| Yes | String(255) | 城市ID |
| payload.rows[x].createTime| Yes | String(255) | 记录创建时间 |
| payload.rows[x].customerHouseId| Yes | String(255) | 客户房源ID |
| payload.rows[x].floors| Yes | String(255) | 楼层数 |
| payload.rows[x].houseLayout| Yes | String(255) | 房源布局 |
| payload.rows[x].houseName| Yes | String(255) | 房源名 |
| payload.rows[x].houseType| Yes | String(255) | 房源类型 |
| payload.rows[x].id| Yes | String(255) | ID |
| payload.rows[x].isFreeze| Yes | String(255) | 是否冻结中 |
| payload.rows[x].lastHistoryId| Yes | String(255) | 最新的历史记录的ID |
| payload.rows[x].lastModifyTime| Yes | String(255) | 最近的更改时间 |
| payload.rows[x].lockedBy| Yes | String(255) | 被谁锁定 |
| payload.rows[x].lockUntil| Yes | String(255) | 锁定到 |
| payload.rows[x].packageId| Yes | String(255) | 数据包ID |
| payload.rows[x].points| Yes | String(255) | 点位数 |
| payload.rows[x].rooms| Yes | String(255) | 房间数 |
| payload.rows[x].serviceId| Yes | String(255) | 服务ID |
| payload.rows[x].serviceType| Yes | String(255) | 服务类型 |
| payload.rows[x].taskState| Yes | String(255) | 任务状态 |
| payload.rows[x].uploadTime| Yes | String(255) | 上传时间 |
| payload.rows[x].captureTime| Yes | String(255) | 拍摄时间，如果拍摄时间异常，会采用上传时间 |
| payload.rows[x].userBalanceId| Yes | String(255) | 使用的余额ID |
| payload.rows[x].userComments| Yes | String(255) | 用户备注 |
| payload.rows[x].path| Yes | String(255) | 用户ID |
| payload.rows[x].userId| Yes | String(255) | 用户ID |
| payload.rows[x].userName| Yes | String(255) | 用户名 |
| payload.rows[x].comments| Yes | String(255) | 系统备注 |
| payload.rows[x].notifyResult| Yes | String(255) | 通知状态（通知客户自己的） |
| payload.rows[x].domain| Yes | String(255) | 数据包的Domain |

## Schema
```json
{
    "state": 200,
    "payload": {
        "total": 1901,
        "rows": [
            {
                "bucket": "vrhouse-test",
                "createTime": "2020-03-18T03:27:27",
                "customerHouseId": "asdfga",
                "floors": 1,
                "houseName": "t2",
                "id": "df7cc2edda5b4d5b8ea7895f0eb5ef38",
                "packageId": "LiangfangTest1_258de0ba-6520-47f4-9262-fed6ca2e04c4",
                "points": 1,
                "rooms": 1,
                "taskState": 50000,
                "uploadTime": "2020-03-18T03:28:54",
                "captureTime" : "2020-03-18T03:28:54",
                "userComments": null,
                "userId": "de2ffbb7787744248194120a76ec92ac",
                "comments": null,
                "domain": "www.123kanfang.com"
            },
            {
                "bucket": "vrhouse-test",
                "createTime": "2020-03-17T09:26:49",
                "customerHouseId": "zcl",
                "floors": 1,
                "houseName": "单房间流程测试317",
                "id": "02a47b088cdf4de6a33c5b5ddf4cb5c5",
                "packageId": "LiangfangTest1_1a2c56f3-489d-4861-ab51-9e202acbee30",
                "points": 1,
                "rooms": 1,
                "taskState": 50000,
                "uploadTime": "2020-03-17T09:26:53",
                "captureTime" : "2020-03-18T03:28:54",
                "userComments": null,
                "userId": "de2ffbb7787744248194120a76ec92ac",
                "comments": null,
                "domain": "www.123kanfang.com"
            }
        ]
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
