# 加密说明\(Java SDK\)<a name="obs_21_1902"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

OBS Java SDK支持服务端加密的接口见下表：

|**OBS Java SDK接口方法**|**说明**|**支持加密类型**|
|--|--|--|
|ObsClient.putObject|上传对象时设置加密算法、密钥，对对象启用服务端加密。|SSE-KMSSSE-CSSE-OBS|
|ObsClient.getObject|具有KMS Administrator权限的用户可直接下载KMS加密对象，后端解密后返回。(SSE-KMS)下载对象时设置解密算法、密钥，用于解密对象。（SSE-C）|SSE-KMSSSE-CSSE-OBS|
|ObsClient.copyObject|复制对象时设置源对象的解密算法、密钥，用于解密源对象。复制对象时设置目标对象的加密算法、密钥，对目标对象启用加密算法。|SSE-KMSSSE-C|
|ObsClient.getObjectMetadata|获取对象元数据时设置解密算法、密钥，用于解密对象。|SSE-CSSE-OBS|
|ObsClient.initiateMultipartUpload|初始化分段上传任务时设置加密算法、密钥，对分段上传任务最终生成的对象启用服务端加密。|SSE-KMSSSE-C|
|ObsClient.uploadPart|上传段时设置加密算法、密钥，对分段数据启用服务端加密。|SSE-C|
|ObsClient.copyPart|复制段时设置源对象的解密算法、密钥，用于解密源对象。复制段时设置目标段的加密算法、密钥，对目标段启用加密算法。|SSE-C|


