# 如果桶内已存在同名对象，如何判定覆盖上传成功？\(Java SDK\)<a name="obs_21_2117"></a>

上传完成后，您可以调用ObsClient.getObjectMetadata接口获取目标对象大小和最后修改时间，再与数据源进行比较，如果两者大小一致且目标对象的最后修改时间晚于数据源的最后修改时间则表明上传成功，否则上传失败。ObsClient.getObjectMetadata接口的使用可参见[18.4-获取对象元数据](获取对象元数据(Java-SDK).md)。

