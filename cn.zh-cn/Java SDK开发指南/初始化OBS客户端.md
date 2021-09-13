# 初始化OBS客户端<a name="obs_21_0107"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。[接口参考文档](https://obssdk.obs.cn-north-1.myhuaweicloud.com/apidoc/cn/java/index.html)详细介绍了每个接口的参数和使用方法。

向OBS发送任一HTTP/HTTPS请求之前，必须先创建一个ObsClient实例：

```
String endPoint = "https://your-endpoint";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";
// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
 
// 使用访问OBS
        
// 关闭obsClient
obsClient.close();
```

>![](public_sys-resources/icon-note.gif) **说明：** 
>更多关于OBS客户端初始化的操作请参考“初始化”章节。

