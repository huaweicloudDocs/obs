# 如何进行分段下载？\(Java SDK\)<a name="obs_21_2115"></a>

在下载对象时，您可以指定下载对象的某一范围内的数据进行分段下载，步骤如下：

1.  您需要以AK、SK、Endpoint先初始化一个客户端ObsClient；
2.  指定桶名和对象名初始化一个GetObjectRequest请求，您可以通过GetObjectRequest.setRangeStart和GetObjectRequest.setRangeEnd接口设置将要下载的对象数据的开始和结束范围；
3.  通过ObsClient.getObject接口发送步骤2的GetObjectRequest请求来进行分段下载。

详细操作可参见[范围下载](范围下载(Java-SDK).md)。

