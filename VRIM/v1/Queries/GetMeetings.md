# 功能介绍
**根据123的appKey/用户的Path/UserId来获取会议记录**

# URI
生产：https://im.123kanfang.com/IM/GetMeetings  
测试：https://im-test.123kanfang.com/IM/GetMeetings


# Method
**GET**

# 身份认证

None


# 请求头
| 参数         | 可空 | 参数类型 | 描述                                      |
| ------------ | ---- | -------- | ----------------------------------------- |
| Content-Type | No   | String   | 值应为：application/x-www-form-urlencoded |


# 请求参数
| 字段名    | 可空 | 数据类型   | 描述         |
| --------- | ---- | ---------- | ------------ |
| pageIndex | No   | int        | 第几页       |
| pageSize  | No   | int        | 每页的数据量 |
| app       | Yes  | string(32) | 123的AppKey  |
| path      | Yes  | string(32) | 用户架构路径 |
| userId    | Yes  | string(32) | 用户userId   |

备注： app、path和userId三个参数必须并且只能选其一

# 正确响应

| 字段名                    | 可空 | 数据类型 | 描述                                         |
| ------------------------- | ---- | -------- | -------------------------------------------- |
| state                     | No   | Int      | [返回状态](../Agreement/APIResponseState.md) |
| payload                   | No   | Object   | 返回的数据载体                               |
| payload.total             | No   | int      | 结果总和                                     |
| payload.pageIndex         | No   | Int      | 第几页                                       |
| payload.pageSize          | No   | int      | 每页数据量                                   |
| payload.rows              | No   | Array    | 分页数据数组                                 |
| payload.rows[x]           | No   | Object   | 数据对象                                     |
| payload.rows[x].index     | No   | int      | 在该页数据中是第几个                         |
| payload.rows[x].packageId | No   | string   | 房源packageId                                |
| payload.rows[x].startTime | No   | string   | 会议开始时间                                 |
| payload.rows[x].endTime   | No   | string   | 会议结束时间                                 |
| payload.rows[x].app       | No   | string   | 会议对应的123appKey                          |


## Schema
```json
{
    "state": 200,
    "payload": {
        "total": 79,
        "pageIndex": 1,
        "pageSize": 5,
        "rows": [
            {
                "index": 0,
                "packageId": "8144b7ff-491d-42b9-80d2-ed83d3a4711b",
                "startTime": "2020-03-30T20:28:00",
                "endTime": "2020-03-30T20:28:30",
                "confrId": "13H0545LENTF0470BUD00C225387",
                "app": "1109200303019897#kanfangtest",
                "path": null
            },
            {
                "index": 1,
                "packageId": "8144b7ff-491d-42b9-80d2-ed83d3a4711b",
                "startTime": "2020-03-30T20:21:20",
                "endTime": "2020-03-30T20:23:20",
                "confrId": "13H05522QATF047EEHD00C225215",
                "app": "1109200303019897#kanfangtest",
                "path": null
            },
            {
                "index": 2,
                "packageId": "8144b7ff-491d-42b9-80d2-ed83d3a4711b",
                "startTime": "2020-03-30T20:00:47",
                "endTime": "2020-03-30T20:02:47",
                "confrId": "13H05522QKTF047B54H00C225304",
                "app": "1109200303019897#kanfangtest",
                "path": null
            },
            {
                "index": 3,
                "packageId": "8144b7ff-491d-42b9-80d2-ed83d3a4711b",
                "startTime": "2020-03-30T19:57:24",
                "endTime": "2020-03-30T19:57:54",
                "confrId": "13H05522QKTF047B54H00C225302",
                "app": "1109200303019897#kanfangtest",
                "path": null
            },
            {
                "index": 4,
                "packageId": "8144b7ff-491d-42b9-80d2-ed83d3a4711b",
                "startTime": "2020-03-30T19:51:36",
                "endTime": "2020-03-30T19:56:05",
                "confrId": "13H05522N8TF0472GIQ00C225167",
                "app": "1109200303019897#kanfangtest",
                "path": null
            }
        ]
    }
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