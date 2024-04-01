# 其他高频问题汇总\(Java SDK\)<a name="obs_21_0302"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## SignatureDoesNotMatch签名不匹配<a name="section4631239543"></a>

```
HTTP Code: 403
Error Code: SignatureDoesNotMatch
```

此类错误一般有三种原因：

1.  初始化ObsClient时传入的SK有误，解决方法：检查SK，确保正确；
2.  旧版本OBS Java SDK的BUG，解决方法：升级SDK到最新版本；
3.  OBS Java SDK 2.1.x版本与其依赖库Apache HttpClient的兼容性问题，解决方法：使用固定版本的依赖库，httpcore-4.4.4和httpclient-4.5.3。

## MethodNotAllowed方法不允许<a name="section192357412354"></a>

```
HTTP Code: 405
Error Code: MethodNotAllowed
```

此错误一般是请求的OBS服务端未上线ObsClient接口依赖的特性，请联系OBS运维团队进行进一步确认。

## BucketAlreadyOwnedByYou创桶失败<a name="section874818289439"></a>

```
HTTP Code: 409
Error Code: BucketAlreadyOwnedByYou
```

OBS中的桶要求全局唯一，即使在不同区域，也不允许出现同名桶。解决方法：如果调用ObsClient.createBucket接口出现该异常，请确认该桶是否已存在。您可通过如下两种方式判断该桶是否已存在。

方式一（推荐）：调用ObsClient.listBuckets接口查询您拥有的全部桶列表后判断该桶是否已经存在；

方式二：调用ObsClient.headBucket接口判断该桶是否已经存在。

>![](public_sys-resources/icon-note.gif) **说明：** 
>ObsClient.headBucket接口只能访问到当前区域下的桶，而ObsClient.listBuckets接口能访问到所有区域下的桶。

## BucketAlreadyExists创桶失败<a name="section152381811441"></a>

```
HTTP Code: 409
Error Code: BucketAlreadyExists
```

OBS中的桶要求全局唯一，即使在不同区域，也不允许出现同名桶。解决方法：如果调用ObsClient.createBucket接口出现该异常，表明其他用户已创建了该桶，请换一个桶名后重新创建。

## 连接超时<a name="section58191624113616"></a>

```
HTTP Code: 408
Caused by: java.net.ConnectException: Connection timed out: connect
	at java.net.DualStackPlainSocketImpl.waitForConnect(Native Method)
	at java.net.DualStackPlainSocketImpl.socketConnect(DualStackPlainSocketImpl.java:85)
```

此类错误一般有三种原因：

1.  初始化ObsClient时传入的Endpoint有误，解决方法：检查Endpoint，确保正确；
2.  客户端到OBS服务端的网络异常，导致无法访问，解决方法：检查客户端到OBS服务端的网络健康状况；
3.  DNS解析出的OBS服务域名无法访问，解决方法：联系OBS运维团队。

## 读写超时<a name="section885063114315"></a>

```
HTTP Code: 408
Error Code:RequestTimeOut
Caused by: java.net.SocketTimeoutException: timeout
	at okio.Okio$4.newTimeoutException(Okio.java:232)
	at okio.AsyncTimeout.exit(AsyncTimeout.java:285)
	at okio.AsyncTimeout$2.read(AsyncTimeout.java:241)
```

此类错误一般有两种原因：

1.  客户端到OBS服务端的网络时延过大，解决方法：检查客户端到OBS服务端的网络健康状况；
2.  客户端到OBS服务端的网络异常，导致无法访问，解决方法：检查客户端到OBS服务端的网络健康状况。

## 异常返回值为-1<a name="section49507108126"></a>

```
HTTP Code: -1
```

此类错误一般有三种原因：

1.  使用了旧版的OBS Java SDK并且发生了连接超时或读写超时的异常，解决方法：参见[连接超时](#section58191624113616)和[读写超时](#section885063114315)的解决方法；
2.  旧版OBS Java SDK的BUG，解决方法：升级到最新版本的SDK，可以从[这里](https://github.com/huaweicloud/huaweicloud-sdk-java-obs)下载最新版本；
3.  服务端返回了异常的结果，导致SDK解析返回结果时出现了不可预期的错误，解决方法：尝试从日志中获取OBS服务端请求ID，并联系OBS运维团队。

## ObsException中无法获取错误码<a name="section19229172110579"></a>

此类错误一般有两种原因：

1.  调用ObsClient.getBucketMetadata或ObsClient.getObjectMetadata报错，此种场景下由于后台使用的是HEAD请求，服务端不会返回错误码，解决方法：使用ObsException.getResponseCode获取HTTP状态码，根据状态码分析可能原因，如403一般代表无权限访问，404一般代表桶或对象不存在；如无法定位原因，可从ObsException中获取OBS服务端请求ID后联系OBS运维团队；
2.  初始化ObsClient时传入的Endpoint通过DNS解析后的IP不是有效的OBS服务端，解决方法：检查Endpoint配置是否正确，如Endpoint确认无误，联系OBS运维团队。

## UnknownHostException域名无法解析异常<a name="section1768032011516"></a>

```
Caused by: java.net.UnknownHostException: bucketname.unknowndomain.com
	at java.net.Inet6AddressImpl.lookupAllHostAddr(Native Method)
	at java.net.InetAddress$1.lookupAllHostAddr(InetAddress.java:901)
	at java.net.InetAddress.getAddressesFromNameService(InetAddress.java:1293)
```

此类错误一般有两种原因：

1.  初始化ObsClient时传入的Endpoint有误，解决方法：检查Endpoint，确保正确；
2.  DNS无法解析OBS服务域名，解决方法：联系OBS运维团队。

## NullPointException空指针异常<a name="section35061634105616"></a>

```
Exception in thread "main" java.lang.NullPointerException
	at com.obs.services.internal.RestStorageService.isCname(RestStorageService.java:1213)
	at com.obs.services.ObsClient.doActionWithResult(ObsClient.java:2805)
```

此类错误一般有两种原因：

1.  使用ObsClient.close接口关闭ObsClient后，再次调用ObsClient的其他接口，解决方法：仅在应用程序退出前调用ObsClient.close接口释放资源；
2.  旧版OBS Java SDK的BUG，解决方法：升级到最新版本的SDK，可以从[这里](https://github.com/huaweicloud/huaweicloud-sdk-java-obs)下载最新版本。

## 连接泄露问题<a name="section11533121316519"></a>

```
A connection to xxx was leaked. Did you forget to close a response body?
```

此错误通常是调用ObsClient.getObject接口获取下载对象的数据流后未正常关闭，解决方法：确保在finally语句块中调用了ObsObject.getObjectContent.close方法关闭连接。

## 升级SDK后okhttp报错问题<a name="section11288121120465"></a>

```
Exception in thread "main" java.lang.NoSuchMethodError: 'okhttp3.RequestBody okhttp3.RequestBody.create(java.lang.String, okhttp3.MediaType)'
	at com.obs.services.internal.RestConnectionService.createRequestBuilder(RestConnectionService.java:157)
	at com.obs.services.internal.RestConnectionService.setupConnection(RestConnectionService.java:148)
	at com.obs.services.internal.RestConnectionService.setupConnection(RestConnectionService.java:124)
	at com.obs.services.internal.RestStorageService.performRequest(RestStorageService.java:395)
	at com.obs.services.internal.RestStorageService.performRequest(RestStorageService.java:388)
```

此报错是因为升级SDK后okhttp使用了老版本的原因，请参考[依赖缺失和依赖冲突的解决\(Java SDK\)](依赖缺失和依赖冲突的解决(Java-SDK).md)  ，升级okhttp到指定版本。

## 升级SDK后报错StackOverflowError问题<a name="section1845718251467"></a>

```
Caused by: java.lang.StackOverflowError
	at sun.misc.URLClassPath.getResource(URLClassPath.java:211) ~[?:1.8.0_91]
	at java.net.URLClassLoader$1.run(URLClassLoader.java:365) ~[?:1.8.0_91]
	at java.net.URLClassLoader$1.run(URLClassLoader.java:362) ~[?:1.8.0_91]
	at java.security.AccessController.doPrivileged(Native Method) ~[?:1.8.0_91]
	at java.net.URLClassLoader.findClass(URLClassLoader.java:361) ~[?:1.8.0_91]
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424) ~[?:1.8.0_91]
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357) ~[?:1.8.0_91]
	at org.apache.catalina.loader.WebappClassLoaderBase.loadClass(WebappClassLoaderBase.java:1806) 
```

检查jvm参数xss， 建议将xss参数设置为1M。xss是jvm启动的每个线程分配的内存大小，默认JDK1.4中是256K，JDK1.5+中是1M。

## 报错SSL peer shut down incorrectly<a name="section1169865521020"></a>

```
javax.net.ssl.SSLException: SSL peer shut down incorrectly
	at sun.security.ssl.InputRecord.readV3Record(InputRecord.java:596)
	at sun.security.ssl.InputRecord.read(InputRecord.java:532)
	at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:975)
	at sun.security.ssl.SSLSocketImpl.readDataRecord(SSLSocketImpl.java:933)
	at sun.security.ssl.AppInputStream.read(AppInputStream.java:105)
	at obs.shaded.okio.Okio$2.read(Okio.java:140)
	at obs.shaded.okio.AsyncTimeout$2.read(AsyncTimeout.java:237)
	at obs.shaded.okio.RealBufferedSource.read(RealBufferedSource.java:51)
	at obs.shaded.okhttp3.internal.http1.Http1ExchangeCodec$AbstractSource.read(Http1ExchangeCodec.java:389)
	at obs.shaded.okhttp3.internal.http1.Http1ExchangeCodec$FixedLengthSource.read(Http1ExchangeCodec.java:427)
	at obs.shaded.okhttp3.internal.connection.Exchange$ResponseBodySource.read(Exchange.java:286)
	at obs.shaded.okio.RealBufferedSource$1.read(RealBufferedSource.java:447)
	at java.util.zip.InflaterInputStream.fill(InflaterInputStream.java:238)
	at java.util.zip.InflaterInputStream.read(InflaterInputStream.java:158)
	at java.util.zip.GZIPInputStream.read(GZIPInputStream.java:117)
	at sun.nio.cs.StreamDecoder.readBytes(StreamDecoder.java:284)
	at sun.nio.cs.StreamDecoder.implRead(StreamDecoder.java:326)
	at sun.nio.cs.StreamDecoder.read(StreamDecoder.java:178)
	at java.io.InputStreamReader.read(InputStreamReader.java:184)
	at java.io.BufferedReader.fill(BufferedReader.java:161)
	at java.io.BufferedReader.readLine(BufferedReader.java:324)
	at java.io.BufferedReader.readLine(BufferedReader.java:389)
```

客户端下载读取文件流时，请不要按行读取，可参考[流式下载](流式下载(Java-SDK).md)的Demo。

## 其他问题<a name="section730245411517"></a>

请参考[FAQ](常见问题(Java-SDK).md)，查看更多问题的解决方法。

