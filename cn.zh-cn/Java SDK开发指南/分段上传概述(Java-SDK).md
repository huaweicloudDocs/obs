# 分段上传概述\(Java SDK\)<a name="obs_21_0614"></a>

## 功能说明<a name="section175591754133514"></a>

对于较大文件上传，可以切分成段上传。用户可以在如下的应用场景内（但不仅限于此），使用分段上传的模式：

-   上传超过100MB大小的文件。
-   网络条件较差，和OBS服务端之间的链接经常断开。
-   上传前无法确定将要上传文件的大小。

使用分段上传具有以下优势：

-   提高吞吐量——您可以使用并行上传段以提高吞吐量。
-   从任何网络问题中快速恢复——较小的段大小可以将由于网络错误而需重启失败的上传所产生的影响降至最低。
-   暂停和恢复对象上传——您可以随时上传对象段。启动多段上传后，不存在过期期限；您必须显式地完成或取消多段上传任务。
-   在得知最终对象大小之前开始上传——您可以在创建对象的同时上传对象。

分段上传分为如下3个步骤：

1.  [初始化分段上传任务（ObsClient.initiateMultipartUpload）](初始化分段上传任务(Java-SDK).md)。
2.  [逐个或并行上传段（ObsClient.uploadPart）](上传段(Java-SDK).md)。
3.  [合并段（ObsClient.completeMultipartUpload）](合并段(Java-SDK).md)或[取消分段上传任务\(ObsClient.abortMultipartUpload\)](取消分段上传任务(Java-SDK).md)。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

