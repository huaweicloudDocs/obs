# 如何获取对象URL？<a name="obs_21_2111"></a>

将桶中的对象权限设置为匿名用户读取权限后，可通过对象的URL直接下载该对象。获取对象URL的方式如下：

方式一，接口查询，ObsClient上传对象后会返回PutObjectResult对象，通过调用该对象的getObjectUrl接口可获取上传对象的URL。示例代码如下：

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";
// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
// 调用putObject接口上传对象并获取其返回结果
PutObjectResult result = obsClient.putObject("bucketname", "objectname", new File("localfile"));
// 读取该已上传对象的URL
System.out.println("\t" + result.getObjectUrl());
```

方式二，按**https://**_**桶名.域名/文件夹目录层级/对象名**的方式进行拼接。_

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   如果该对象存在于桶的根目录下，则链接地址将不需要有文件夹目录层级；
>-   各区域对应的域名可以从[这里](https://developer.huaweicloud.com/endpoint?OBS)的终端节点查看。
>-   例如需访问区域为“华北-北京四”的桶名为“testbucket”中“test”文件夹下对象名为“test.txt”的对象，则该对象的URL为https://testbucket.obs.cn-north-4.myhuaweicloud.com/test/test.txt。

