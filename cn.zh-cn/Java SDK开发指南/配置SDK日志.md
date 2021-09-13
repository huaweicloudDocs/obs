# 配置SDK日志<a name="obs_21_0204"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。[接口参考文档](https://obssdk.obs.cn-north-1.myhuaweicloud.com/apidoc/cn/java/index.html)详细介绍了每个接口的参数和使用方法。

OBS Java SDK基于Apache Log4j2开源库提供了日志功能，SDK默认会将WARN级别的日志记录到JDK系统变量user.dir所代表的路径下，您可以通过修改日志配置文件定制日志功能。具体步骤如下：

1.  找到OBS Java SDK开发包中的log4j2.xml文件，或在[这里](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/main/resource/log4j2.xml)获取。
2.  根据实际情况修改log4j2.xml中的日志级别和日志存放路径。
3.  将log4j2.xml文件放到classpath根目录，或者调用Log4j2Configurator.setLogConfig直接指定log4j2.xml文件的路径。

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   您可以从[日志分析](日志分析.md)章节获取更多关于SDK日志的信息。
>-   您可以根据实际需要通过修改log4j2.xml文件来配置日志文件权限。

