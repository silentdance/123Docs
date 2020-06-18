## 拍摄前[可选]
* [查看是否有进行中的任务](./GetWorkingTaskByCustomerHouseId.md) [创建拍摄任务方式必选，其他可选]
* [创建拍摄任务](./AssignNewCaptureHouseTask.md) [创建拍摄任务方式必选，其他可选]
* [取消拍摄任务](./CancelCaptureHouseTask.md) [创建拍摄任务方式必选，其他可选]

## 上传后
* [查询任务列表](./GetPage.md) [可选]
* [提交房源制作完成](./FinishHouseTask.md) [可选]
* [客户接收任务状态变更通知](./CustomerReceiveTaskStateChangeNotify.md) [可选]

## 制作完成后[可选]
* [指定客户审核结果](./CustomerAssignReviewResult.md) [可选]
* [废弃某个数据包](./RetireHouseTask.md) [可选]


## 推送相关的通用接口
* [创建通知任务](./AddNewNotifyTaskByPackageID.md) [推送三方平台时必选]
* [当推送异常时的回调接口](./CustomerReceiveNotifyFailedNotify.md) [可选]

## 制作完成后的数据包推送
* [客户接收数据包下载通知](./CustomerReceivePackageDownloadNotify.md)

## 推送安居客[可选]
* [推送前设置安居客编号](./PutAnjukeBianHao.md) [可选]
* 推送安居客的结果回调 [可选]

## 推送房天下[可选]
* [推送前设置房天下的房源数据](./PutFangTianXiaInfo.md)
* [推送房天下的结果回调](./FangTianXiaNotifyCallback.md) [可选]