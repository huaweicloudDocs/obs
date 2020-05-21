# SDK是否支持批量上传、下载或复制对象？<a name="obs_21_2121"></a>

不支持。

目前SDK暂未提供此类接口，您需要自己封装批量上传、下载或复制对象的业务代码。步骤如下：

1.  列举出所有待上传、下载或者复制的对象。可参考[列举对象](列举对象.md)章节，列举待下载的对象。
2.  对列举出的对象调用单个对象的上传（上传对象）、下载（下载对象）或复制（复制对象）接口。

以批量上传对象为例，示例代码如下：

```
String endPoint = "https://your-endpoint";
String ak = "*** Provide your Access Key ***";
String sk = "*** Provide your Secret Key ***";
final String bucketName = "bucketname";
// 定义桶内对象的前缀
final String objectPre = "object/";
// 待上传的文件夹
final String localDirPath = "localDirPath";
final List<File> list = new ArrayList<>();
// 扫描文件夹下所有对象
static void listFiles(File file){
    File[] fs = file.listFiles();
    assert fs != null;
    if (fs.length < 1){
        // 如果是空文件夹也需要上传，将其添加到列表中
        list.add(file);
    }else{
        for (File f:fs){
            if (f.isDirectory()){
                listFiles(f);
            }
            if (f.isFile()){
                // 添加待上传对象到列表中
                list.add(f);
            }
        }
    }
}
// 遍历待上传的文件夹，获取所有待上传对象
File file = new File(localDirPath);
listFiles(file);

// 创建ObsClient实例
final ObsClient obsClient = new ObsClient(ak, sk, endPoint);

// 初始化线程池
ExecutorService executorService = Executors.newFixedThreadPool(20);

// 执行并发上传
for (File f:list){
    executorService.execute(() -> {
        if (f.isDirectory()){
            // 如果是空文件夹，则在桶内创建对应的空文件夹对象
            String remoteObjectKey = objectPre + f.getPath().substring(localDirPath.length() + 1) + "/";
            obsClient.putObject(bucketName, remoteObjectKey, new ByteArrayInputStream(new byte[0]));
        }else{
            String remoteObjectKey = objectPre + f.getPath().substring(localDirPath.length() + 1);
            obsClient.putObject(bucketName, remoteObjectKey, new File(f.getPath()));
        }
    });
}

// 等待上传完成
executorService.shutdown();
while (!executorService.isTerminated())
{
    try
    {
        executorService.awaitTermination(5, TimeUnit.SECONDS);
    }
    catch (InterruptedException e)
    {
        e.printStackTrace();
    }
}
// 关闭obsClient
try {
    obsClient.close();
} catch (IOException e) {
    e.printStackTrace();
}
```

>![](public_sys-resources/icon-note.gif) **说明：**   
>您可以使用多线程并发执行上传/下载/复制操作，以提高效率。  

