# 对象下载简介\(Java SDK\)<a name="obs_21_0701"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

OBS Java SDK提供了丰富的对象下载接口，可以通过以下方式下载对象：

-   [流式下载](流式下载(Java-SDK).md)
-   [范围下载](范围下载(Java-SDK).md)
-   [断点续传下载](断点续传下载(Java-SDK).md)

您可以通过ObsClient.getObject下载对象。

## 请求参数<a name="section123091114385"></a>

|**参数名**|**类型**|**约束**|**说明**|
|--|--|--|--|
|objectKey|String|必选|对象名。|
|bucketName|String|必选|桶名。|
|progressInterval|long|可选|下载进度反馈间隔。例子：1024 * 1024，每下载1MB数据反馈下载进度。|
|progressListener|ProgressListener|可选|设置数据传输监听器，用于获取下载进度。|
|isEncodeHeaders|boolean|可选|是否自动编码请求头，默认是true。|
|userHeaders|HashMap<String, String>|可选|用户头域。|
|ifMatchTag|String|可选|如果对象的ETag值与该参数值相同，则返回对象内容，否则抛出异常。|
|ifNoneMatchTag|String|可选|如果对象的ETag值与该参数值不相同，则返回对象内容，否则抛出异常。|
|ifModifiedSince|Date|可选|如果对象的修改时间晚于该参数值指定的时间，则返回对象内容，否则抛出异常。|
|ifUnmodifiedSince|Date|可选|如果对象的修改时间早于该参数值指定的时间，则返回对象内容，否则抛出异常。|
|imageProcess|String|可选|图片处理参数。|
|rangeStart|Long|可选|范围下载时，指定开始字节。|
|rangeEnd|Long|可选|范围下载时，指定结束字节。|
|replaceMetadata|ObjectRepleaceMetadata|可选|下载对象时重写响应头。|
|sseCHeader|SseCHeader|可选|服务端加密头信息。|
|versionId|String|可选|版本号。|


