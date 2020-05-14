# 功能介绍
**生成编辑链接**

# 编辑器地址
生产：
http://www.123kanfang.com/VRHouseOnline/123kanfang31/client.html
?noCache=true
&hid={hid}
&bucket=vrhouse
&domain=//vrhouse.oss-cn-shanghai.aliyuncs.com/
&token={token}  

测试：http://webresource.123kanfang.com/studioClient-test/client.html
?noCache=true
&hid={hid}
&floorPlanStyles={floorPlanStyles}
&bucket={bucket}
&domain=//{domain}/
&token={token}

# 参数
| 字段名 | 可空 | 数据类型 | 描述 |
| ---- | ---- | ---- | ----|
| hid | No | String(128) | packageId |
| floorPlanStyles | Yes | String(32) | 户型图样式，默认可以不传 |
| bucket | No | String(32) | 当前房源的存储桶（咨询123获取具体的值） |
| domain | No | String(128) | 访问房源数据的域名（咨询123获取具体的值） |
| token | No | String | 当前房源拥有者的token |
