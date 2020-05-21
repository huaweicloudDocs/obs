# 初始化OBS客户端<a name="obs_21_0107"></a>

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

