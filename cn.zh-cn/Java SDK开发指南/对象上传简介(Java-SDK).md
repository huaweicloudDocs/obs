# 对象上传简介\(Java SDK\)<a name="obs_21_0601"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

在OBS中，用户操作的基本数据单元是对象。OBS Java SDK提供了丰富的对象上传接口，可以通过以下方式上传对象：

-   [流式上传](流式上传(Java-SDK).md)
-   [文件上传](文件上传(Java-SDK).md)
-   [分段上传](分段上传(Java-SDK).md)
-   [追加上传](追加上传(Java-SDK).md)
-   [断点续传上传](断点续传上传(Java-SDK).md)
-   [基于表单上传](基于表单上传(Java-SDK).md)

SDK支持上传0KB\~5GB的对象。流式上传、文件上传和追加上传的内容大小不能超过5GB；当上传较大文件时，请使用分段上传，分段上传每段内容大小不能超过5GB；基于表单上传提供了基于浏览器表单上传对象的方式。

如果上传的对象权限设置为匿名用户读取权限，对象上传成功后，匿名用户可通过链接地址访问该对象数据。对象链接地址格式为：https://_桶名.域名/文件夹目录层级/对象名_。如果该对象存在于桶的根目录下，则链接地址将不需要有文件夹目录层级。

