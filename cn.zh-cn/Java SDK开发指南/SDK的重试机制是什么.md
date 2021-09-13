# SDK的重试机制是什么？<a name="obs_21_2109"></a>

SDK通过配置[配置OBS客户端](配置OBS客户端.md)章节中的maxErrorRetry参数来实行重试，默认重试3次，建议值为0到5次之间。当调用ObsClient的接口发生网络连接异常或者服务端返回5XX错误时，SDK会进行指数退避重试。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>-   ObsClient.putObject接口，当数据源是非FileInputStream的其他InputStream时，由于数据流不能回读，当发生IO异常时，SDK不会进行重试，需要上层应用程序自行重试；
>-   ObsClient.getObject接口，当请求成功并返回ObsObject对象后，由于此时已不在SDK的处理逻辑范围，当从ObsObject.getObjectContent读取数据过程中，当发生IO异常时，SDK不会进行重试，需要上层应用程序自行重试。

