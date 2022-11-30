# SDK公共响应头<a name="obs_21_2003"></a>

调用ObsClient类的相关接口成功后，均会返回公共响应头类，即HeaderResponse类实例（或其子类实例），该类包含了HTTP/HTTPS的响应头信息。

处理公共响应头的示例代码如下：

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";
// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
HeaderResponse response = obsClient.createBucket("bucketname");

// 从公共响应头中获取request-id
System.out.println("\t" + response.getRequestId());

obsClient.close();
```

