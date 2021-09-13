# 配置OBS客户端<a name="obs_21_0203"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。[接口参考文档](https://obssdk.obs.cn-north-1.myhuaweicloud.com/apidoc/cn/java/index.html)详细介绍了每个接口的参数和使用方法。

当使用配置类（ObsConfiguration）创建OBS客户端（ObsClient）时，您可通过ObsConfiguration配置类对ObsClient进行配置，可配置代理、连接超时、最大连接数等参数。通过ObsConfiguration可以设置的参数见下表：

<a name="table10831182114445"></a>
<table><thead align="left"><tr id="row683212154419"><th class="cellrowborder" valign="top" width="22.772277227722775%" id="mcps1.1.5.1.1"><p id="p118329219446"><a name="p118329219446"></a><a name="p118329219446"></a><strong id="b9209101404510"><a name="b9209101404510"></a><a name="b9209101404510"></a>参数</strong></p>
</th>
<th class="cellrowborder" valign="top" width="26.732673267326735%" id="mcps1.1.5.1.2"><p id="p12832121184414"><a name="p12832121184414"></a><a name="p12832121184414"></a><strong id="b21682223450"><a name="b21682223450"></a><a name="b21682223450"></a>描述</strong></p>
</th>
<th class="cellrowborder" valign="top" width="33.663366336633665%" id="mcps1.1.5.1.3"><p id="p14832182111441"><a name="p14832182111441"></a><a name="p14832182111441"></a><strong id="b1910122517458"><a name="b1910122517458"></a><a name="b1910122517458"></a>方法</strong></p>
</th>
<th class="cellrowborder" valign="top" width="16.831683168316832%" id="mcps1.1.5.1.4"><p id="p174671008433"><a name="p174671008433"></a><a name="p174671008433"></a><strong id="b1128413161341"><a name="b1128413161341"></a><a name="b1128413161341"></a>建议值</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row108328217449"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p16832192117441"><a name="p16832192117441"></a><a name="p16832192117441"></a>connectionTimeout</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p0832112144416"><a name="p0832112144416"></a><a name="p0832112144416"></a>建立HTTP/HTTPS连接的超时时间（单位：毫秒）。默认为60000毫秒。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p883232118440"><a name="p883232118440"></a><a name="p883232118440"></a>ObsConfiguration.setConnectionTimeout</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p104681806437"><a name="p104681806437"></a><a name="p104681806437"></a>[10000, 60000]</p>
</td>
</tr>
<tr id="row48331421104417"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p18833142116449"><a name="p18833142116449"></a><a name="p18833142116449"></a>socketTimeout</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p283372118449"><a name="p283372118449"></a><a name="p283372118449"></a>Socket层传输数据的超时时间（单位：毫秒）。默认为60000毫秒。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p583302194414"><a name="p583302194414"></a><a name="p583302194414"></a>ObsConfiguration.setSocketTimeout</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p94681501436"><a name="p94681501436"></a><a name="p94681501436"></a>[10000, 60000]</p>
</td>
</tr>
<tr id="row724815598281"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p22491159192810"><a name="p22491159192810"></a><a name="p22491159192810"></a>idleConnectionTime</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p1825065982818"><a name="p1825065982818"></a><a name="p1825065982818"></a>如果空闲时间超过此参数的设定值，则关闭连接（单位：毫秒）。默认为30000毫秒。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p102505598288"><a name="p102505598288"></a><a name="p102505598288"></a>ObsConfiguration.setIdleConnectionTime</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p74687016437"><a name="p74687016437"></a><a name="p74687016437"></a>默认</p>
</td>
</tr>
<tr id="row6502192717387"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p1050292773816"><a name="p1050292773816"></a><a name="p1050292773816"></a>maxIdleConnections</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p550282717384"><a name="p550282717384"></a><a name="p550282717384"></a>连接池中最大空闲连接数，默认值：1000。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p13502102712382"><a name="p13502102712382"></a><a name="p13502102712382"></a>ObsConfiguration.setMaxIdleConnections</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p1150232793815"><a name="p1150232793815"></a><a name="p1150232793815"></a>N/A</p>
</td>
</tr>
<tr id="row168335218440"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p1883352154411"><a name="p1883352154411"></a><a name="p1883352154411"></a>maxConnections</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p983302124412"><a name="p983302124412"></a><a name="p983302124412"></a>最大允许的HTTP并发请求数。默认为1000。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p08335217449"><a name="p08335217449"></a><a name="p08335217449"></a>ObsConfiguration.setMaxConnections</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p44681909435"><a name="p44681909435"></a><a name="p44681909435"></a>默认</p>
</td>
</tr>
<tr id="row16833921104414"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p178331621154413"><a name="p178331621154413"></a><a name="p178331621154413"></a>maxErrorRetry</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p78331121164412"><a name="p78331121164412"></a><a name="p78331121164412"></a>请求失败（请求异常、服务端报500或503错误等）后最大的重试次数。默认3次。</p>
<div class="note" id="note15205658102314"><a name="note15205658102314"></a><a name="note15205658102314"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p1157424292417"><a name="p1157424292417"></a><a name="p1157424292417"></a>该参数对于上传对象和下载对象接口时，当上传或下载已经进入数据流处理阶段后产生异常中断，此时将不会重试。</p>
</div></div>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p188331621114420"><a name="p188331621114420"></a><a name="p188331621114420"></a>ObsConfiguration.setMaxErrorRetry</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p10468100174315"><a name="p10468100174315"></a><a name="p10468100174315"></a>[0, 5]</p>
</td>
</tr>
<tr id="row15833621134411"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p68331421164412"><a name="p68331421164412"></a><a name="p68331421164412"></a>endPoint</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p1183382110444"><a name="p1183382110444"></a><a name="p1183382110444"></a>连接OBS的服务地址。可包含协议类型、域名、端口号。示例：https://your-endpoint:443。（出于安全性考虑，建议使用https协议）</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p19833132114442"><a name="p19833132114442"></a><a name="p19833132114442"></a>ObsConfiguration.setEndPoint</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p144683084318"><a name="p144683084318"></a><a name="p144683084318"></a>N/A</p>
</td>
</tr>
<tr id="row18901163111115"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p19012313115"><a name="p19012313115"></a><a name="p19012313115"></a>httpProxy</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p8901131101112"><a name="p8901131101112"></a><a name="p8901131101112"></a>HTTP代理配置。默认为空。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p79011831151119"><a name="p79011831151119"></a><a name="p79011831151119"></a>ObsConfiguration.setHttpProxy</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p204686074315"><a name="p204686074315"></a><a name="p204686074315"></a>N/A</p>
</td>
</tr>
<tr id="row0600952111317"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p4600552171310"><a name="p4600552171310"></a><a name="p4600552171310"></a>validateCertificate</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p8601105251313"><a name="p8601105251313"></a><a name="p8601105251313"></a>是否验证服务端证书。默认为false。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p1660135219139"><a name="p1660135219139"></a><a name="p1660135219139"></a>ObsConfiguration.setValidateCertificate</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p2046811054310"><a name="p2046811054310"></a><a name="p2046811054310"></a>N/A</p>
</td>
</tr>
<tr id="row1376292910153"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p1176217292152"><a name="p1176217292152"></a><a name="p1176217292152"></a>verifyResponseContentType</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p1356155616158"><a name="p1356155616158"></a><a name="p1356155616158"></a>是否验证响应头信息的ContentType。默认为true。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p2762162918151"><a name="p2762162918151"></a><a name="p2762162918151"></a>ObsConfiguration.setVerifyResponseContentType</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p184682044316"><a name="p184682044316"></a><a name="p184682044316"></a>默认</p>
</td>
</tr>
<tr id="row133933491190"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p16393124951913"><a name="p16393124951913"></a><a name="p16393124951913"></a>readBufferSize</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p196381625164516"><a name="p196381625164516"></a><a name="p196381625164516"></a>从Socket流下载对象的缓存大小（单位：字节），-1表示不设置缓存。默认为-1。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p12393249181914"><a name="p12393249181914"></a><a name="p12393249181914"></a>ObsConfiguration.setReadBufferSize</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p11711132441412"><a name="p11711132441412"></a><a name="p11711132441412"></a>N/A</p>
</td>
</tr>
<tr id="row19437155319193"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p17437165381918"><a name="p17437165381918"></a><a name="p17437165381918"></a>writeBufferSize</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p8437155391917"><a name="p8437155391917"></a><a name="p8437155391917"></a>上传对象到Socket流时的缓存大小（单位：字节），-1表示不设置缓存。默认为-1。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p143712534192"><a name="p143712534192"></a><a name="p143712534192"></a>ObsConfiguration.setWriteBufferSize</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p18726424171419"><a name="p18726424171419"></a><a name="p18726424171419"></a>N/A</p>
</td>
</tr>
<tr id="row8668194319411"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p2422925171916"><a name="p2422925171916"></a><a name="p2422925171916"></a>socketWriteBufferSize</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p1042222520190"><a name="p1042222520190"></a><a name="p1042222520190"></a>Socket发送缓冲区大小（单位：字节），对应java.net.SocketOptions.SO_SNDBUF参数。默认为-1表示不设置。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p1642219254194"><a name="p1642219254194"></a><a name="p1642219254194"></a>ObsConfiguration.setSocketWriteBufferSize</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p2468803435"><a name="p2468803435"></a><a name="p2468803435"></a>默认</p>
</td>
</tr>
<tr id="row756217410416"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p10703134581918"><a name="p10703134581918"></a><a name="p10703134581918"></a>socketReadBufferSize</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p12703154518195"><a name="p12703154518195"></a><a name="p12703154518195"></a>Socket接收缓冲区大小（单位：字节），对应java.net.SocketOptions.SO_RCVBUF参数。默认为-1表示不设置。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p1870394517199"><a name="p1870394517199"></a><a name="p1870394517199"></a>ObsConfiguration.setSocketReadBufferSize</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p134682074316"><a name="p134682074316"></a><a name="p134682074316"></a>默认</p>
</td>
</tr>
<tr id="row351654320425"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p9150451113118"><a name="p9150451113118"></a><a name="p9150451113118"></a>keyManagerFactory</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p1515085163115"><a name="p1515085163115"></a><a name="p1515085163115"></a>用于生成javax.net.ssl.KeyManager的工厂。默认为空。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p12150351193111"><a name="p12150351193111"></a><a name="p12150351193111"></a>ObsConfiguration.setKeyManagerFactory</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p915065153117"><a name="p915065153117"></a><a name="p915065153117"></a>N/A</p>
</td>
</tr>
<tr id="row16421154464211"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p12732952143117"><a name="p12732952143117"></a><a name="p12732952143117"></a>trustManagerFactory</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p773265212313"><a name="p773265212313"></a><a name="p773265212313"></a>用于生成javax.net.ssl.TrustManager的工厂。默认为空。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p1573225212316"><a name="p1573225212316"></a><a name="p1573225212316"></a>ObsConfiguration.setTrustManagerFactory</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p1873345213111"><a name="p1873345213111"></a><a name="p1873345213111"></a>N/A</p>
</td>
</tr>
<tr id="row11154445144220"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p873865317311"><a name="p873865317311"></a><a name="p873865317311"></a>isStrictHostnameVerification</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p173816533312"><a name="p173816533312"></a><a name="p173816533312"></a>是否严格验证服务端主机名。默认为false。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p6738253173118"><a name="p6738253173118"></a><a name="p6738253173118"></a>ObsConfiguration.setIsStrictHostnameVerification</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p8738853143110"><a name="p8738853143110"></a><a name="p8738853143110"></a>N/A</p>
</td>
</tr>
<tr id="row1057116265167"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p175710264168"><a name="p175710264168"></a><a name="p175710264168"></a>keepAlive</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p20571102616165"><a name="p20571102616165"></a><a name="p20571102616165"></a>是否使用长连接访问OBS服务。默认为true。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p1571122615167"><a name="p1571122615167"></a><a name="p1571122615167"></a>ObsConfiguration.setKeepAlive</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p1541355710160"><a name="p1541355710160"></a><a name="p1541355710160"></a>N/A</p>
</td>
</tr>
<tr id="row2211614204417"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p171998467395"><a name="p171998467395"></a><a name="p171998467395"></a>cname</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p7199846143912"><a name="p7199846143912"></a><a name="p7199846143912"></a>是否通过自定义域名访问OBS服务。默认为false。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p8199164623919"><a name="p8199164623919"></a><a name="p8199164623919"></a>ObsConfiguration.setCname</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p101996464399"><a name="p101996464399"></a><a name="p101996464399"></a>N/A</p>
</td>
</tr>
<tr id="row179727410"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p129710713116"><a name="p129710713116"></a><a name="p129710713116"></a>sslProvider</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p1697171810"><a name="p1697171810"></a><a name="p1697171810"></a>SSLContext的Provider，默认使用JDK提供的SSLContext。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p109713720117"><a name="p109713720117"></a><a name="p109713720117"></a>ObsConfiguration.setSslProvider</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p785717556115"><a name="p785717556115"></a><a name="p785717556115"></a>N/A</p>
</td>
</tr>
<tr id="row6800048174612"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p980024824618"><a name="p980024824618"></a><a name="p980024824618"></a>httpProtocolType</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p198001748174613"><a name="p198001748174613"></a><a name="p198001748174613"></a>访问OBS服务端时使用的HTTP协议类型。默认为HTTP1.1协议。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p1816948154613"><a name="p1816948154613"></a><a name="p1816948154613"></a>ObsConfiguration.setHttpProtocolType</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p1815213144717"><a name="p1815213144717"></a><a name="p1815213144717"></a>N/A</p>
</td>
</tr>
<tr id="row8503183123119"><td class="cellrowborder" valign="top" width="22.772277227722775%" headers="mcps1.1.5.1.1 "><p id="p1437055362812"><a name="p1437055362812"></a><a name="p1437055362812"></a>httpDispatcher</p>
</td>
<td class="cellrowborder" valign="top" width="26.732673267326735%" headers="mcps1.1.5.1.2 "><p id="p237045313282"><a name="p237045313282"></a><a name="p237045313282"></a>自定义分发器。</p>
</td>
<td class="cellrowborder" valign="top" width="33.663366336633665%" headers="mcps1.1.5.1.3 "><p id="p5370195318281"><a name="p5370195318281"></a><a name="p5370195318281"></a>ObsConfiguration.setHttpDispatcher</p>
</td>
<td class="cellrowborder" valign="top" width="16.831683168316832%" headers="mcps1.1.5.1.4 "><p id="p13714123017294"><a name="p13714123017294"></a><a name="p13714123017294"></a>N/A</p>
</td>
</tr>
</tbody>
</table>

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   建议值为N/A的表示需要根据实际情况进行设置。
>-   如需提高文件上传下载性能，在网络带宽满足的情况下，可对socketWriteBufferSize，sockeReadBufferSize，readBufferSize，writeBufferSize四个参数进行调优。
>-   如网络状况不佳，建议增大connectionTimeout和socketTimeout的值。
>-   如果设置的endPoint不带协议类型，则默认使用HTTPS协议。
>-   出于DNS解析性能和OBS服务可靠性的考虑，不允许将endPoint设置为IP，必须使用域名访问OBS服务。

