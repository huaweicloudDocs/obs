# 日志分析\(Java SDK\)<a name="obs_21_2004"></a>

## 日志开启方式<a name="section1028019596337"></a>

1.  将OBS SDK包中的log4j2.xml文件放到classpath根目录；
2.  或者调用Log4j2Configurator.setLogConfig直接指定log4j2.xml文件的路径。

>![](public_sys-resources/icon-note.gif) **说明：** 
>您可以从OBS Java SDK的发布软件包中获取默认的日志配置文件log4j2.xml，并在该文件基础上进行修改定制。

## 日志路径<a name="section13252175719236"></a>

OBS Java SDK的日志路径是通过log4j2.xml指定的，默认存放于JDK系统变量user.dir所代表的路径下。通常包含三个日志文件：

|**文件名**|**说明**|
|--|--|
|OBS-SDK.interface_north.log|北向日志，OBS Java SDK与用户第三方应用交互的日志记录。|
|OBS-SDK.interface_south.log|南向日志，OBS Java SDK与OBS服务端交互的日志记录。|
|OBS-SDK.access.log|OBS客户端运行日志。|


## 日志内容格式<a name="section857511014255"></a>

SDK日志格式为：日志时间|线程号|日志级别|日志内容。示例如下：

```
#南向日志 
2017-08-21 17:40:07 133|main|INFO |HttpClient cost 157 ms to apply http request
2017-08-21 17:40:07 133|main|INFO |Received expected response code: true
2017-08-21 17:40:07 133|main|INFO |expected code(s): [200, 204].

#北向日志
2017-08-21 17:40:06 820|main|INFO |Storage|1|HTTP+XML|ObsClient||||2017-08-21 17:40:05|2017-08-21 17:40:06|||0|
2017-08-21 17:40:07 136|main|INFO |Storage|1|HTTP+XML|setObjectAcl||||2017-08-21 17:40:06|2017-08-21 17:40:07|||0|
2017-08-21 17:40:07 137|main|INFO |ObsClient [setObjectAcl] cost 312 ms
```

## 日志级别<a name="section474694810253"></a>

当系统出现问题需要定位且当前的日志无法满足要求时，可以通过修改日志的级别来获取更多的信息。其中TRACE日志信息最丰富，ERROR日志信息最少。

具体说明如下：

-   OFF: 关闭级别，如果设置为这个级别，日志打印功能将被关闭。
-   TRACE：跟踪级别，如果设置为这个级别，将打印所有日志信息。通常不建议使用。
-   DEBUG：调试级别，如果设置为这个级别，除了打印INFO级别以上的信息外，还将打印每次HTTP/HTTPS请求和响应的头信息，鉴权算法计算出的StringToSign信息等。
-   INFO：信息级别，如果设置为这个级别，除了打印WARN级别以上的信息外，还将打印HTTP/HTTPS请求的耗时时间，ObsClient接口的耗时时间等。
-   WARN：告警级别，如果设置为这个级别，除了打印ERROR级别以上的信息外，还将打印一些关键事件的信息，如重试请求超过最大次数等。
-   ERROR：错误级别，如果设置为这个级别，仅打印发生异常时的错误信息。

## 设置方式<a name="section3653337785"></a>

以下代码分别为南向日志、北向日志和OBS客户端运行日志设置了不同的日志级别（日志配置文件的全部内容参见log4j2.xml配置文件）：

```
<!-- north log -->
<Logger name="com.obs.services.AbstractClient" level="INFO" additivity="false">
      <AppenderRef ref="NorthInterfaceLogAppender" />
</Logger>
        
<!-- south log -->
<Logger name="com.obs.services.internal.RestStorageService" level="WARN" additivity="false">
       <AppenderRef ref="SouthInterfaceLogAppender" />
</Logger>

<!-- access log -->
<Logger name="com.obs.log.AccessLogger" level="ERROR" additivity="false">
        <AppenderRef ref="AccessLogAppender" />
</Logger>
```

