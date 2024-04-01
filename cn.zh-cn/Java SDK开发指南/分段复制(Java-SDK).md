# 分段复制\(Java SDK\)<a name="obs_21_0810"></a>

## 功能说明<a name="section35694663"></a>

分段复制是分段上传的一种特殊情况，即分段上传任务中的段可以通过复制OBS指定桶中现有对象（或对象的一部分）来实现。

您可以通过ObsClient.copyPart来复制段。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section11169333135513"></a>

-   您必须是桶拥有者或拥有复制对象的权限，才能复制对象。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:PutObject权限，如果使用桶策略则需授予PutObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   用户有待复制的源对象的读权限。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   复制对象操作的请求需要通过头域携带拷贝的原桶和对象信息，不能携带消息实体。
-   支持同区域跨桶复制，不支持跨区域复制。
-   如果待复制的源对象是归档存储类别，则必须先恢复源对象才能进行复制。

## 方法定义<a name="section54232412"></a>

obsClient.copyPart\([CopyPartRequest](#table14455523) [request](#table1210700)\)

## 分段复制请求参数<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|CopyPartRequest|必选|**参数解释：**分段复制对象请求参数，详见CopyPartRequest。|


**表 2**  CopyPartRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|sourceBucketName|String|必选|**参数解释：**源桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|sourceObjectKey|String|必选|**参数解释：**源对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|destinationBucketName|String|必选|**参数解释：**目标桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|destinationObjectKey|String|必选|**参数解释：**目标对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|byteRangeStart|Long|可选|**参数解释：**指定复制源对象的起始位置。**取值范围：**非负整数，单位：字节。**默认取值：**0|
|byteRangeEnd|Long|可选|**参数解释：**指定复制源对象的结束位置。**约束限制：**取值必须大于RangeStart，如果该值大于对象长度-1，实际仍取对象长度-1，单位为字节。**取值范围：**非负整数，单位：字节。**默认取值：**无|
|sseCHeaderSource|SseCHeader|可选|**参数解释：**服务端加密头信息，用于解密源对象。详情参见SseCHeader。|
|sseCHeaderDestination|SseCHeader|可选|**参数解释：**服务端加密头信息，用于加密目标对象。详情参见SseCHeader。**约束限制：**如果客户端的对象上传时，使用了客户提供的加密密钥进行服务端加密，当下载对象时，同样也必须在消息中提供密钥。|
|versionId|String|可选|**参数解释：**源对象的版本号。例如：G001117FCE89978B0000401205D5DC9A。如果源对象存在多个版本，可以指定该参数。**取值范围：**长度为32的字符串。**默认取值：**无|
|partNumber|int|必选|**参数解释：**段号。**取值范围：**取值范围是[1,10000]的非负整数。**默认取值：**无|
|uploadId|String|必选|**参数解释：**分段上传任务的ID，例如：000001648453845DBB78F2340DD460D8。**取值范围：**长度为32的字符串。**默认取值：**无|


**表 3**  SseCHeader

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|algorithm|ServerAlgorithm|必选|**参数解释：**表示服务端加密是SSE-C方式，对象使用SSE-C加密方式。**取值范围：**可选值：AES256，即选择SSE-C方式，使用高级加密标准（Advanced Encryption Standard，AES）加密对象。详见ServerAlgorithm。**默认取值：**无|
|sseAlgorithm|SSEAlgorithmEnum|可选|**参数解释：**加密算法。**约束限制：**只支持AES256。**取值范围：**详见SSEAlgorithmEnum。**默认取值：**无|
|sseCKey|byte[]|必选|**参数解释：**SSE-C方式下加密使用的原始密钥，byte[]形式，该密钥用于加密对象。**默认取值：**无|
|sseCKeyBase64|String|可选|**参数解释：**SSE-C方式下的密钥，由原始密钥经过Base64编码后得到，该密钥用于加密对象。**默认取值：**无|


**表 4**  ServerAlgorithm

|**常量值**|**原始值**|
|--|--|
|AES256|AES256|


**表 5**  SSEAlgorithmEnum

|**常量值**|**原始值**|
|--|--|
|KMS|kms|
|AES256|AES256|


## 分段复制返回结果说明<a name="section19765119121410"></a>

**表 6**  CopyPartResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|partNumber|int|**数解释：**段号。**取值范围：**取值范围是[1,10000]的非负整数。**默认取值：**无|
|etag|String|**参数解释：**对象的etag值，即Base64编码的128位MD5摘要。etag是对象内容的唯一标识，可以通过该值识别对象内容是否有变化。比如上传对象时etag为A，下载对象时etag为B，则说明对象内容发生了变化。etag只反映变化的内容，而不是其元数据。上传的对象或拷贝操作创建的对象，都有唯一的etag。**约束限制：**当对象是服务端加密的对象时，etag值不是对象的MD5值。**取值范围：**长度为32的字符串。**默认取值：**无|
|lastModified|java.util.Date|**参数解释：**目标段的最近一次修改时间。**默认取值：**无|


## 代码示例<a name="section756512211131"></a>

本示例用于复制段，将sourcebucketname源桶下的sourceobjectname对象复制到destbucketname目标桶下的destobjectname对象中。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.CompleteMultipartUploadRequest;
import com.obs.services.model.CopyPartRequest;
import com.obs.services.model.CopyPartResult;
import com.obs.services.model.InitiateMultipartUploadRequest;
import com.obs.services.model.InitiateMultipartUploadResult;
import com.obs.services.model.ObjectMetadata;
import com.obs.services.model.PartEtag;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;
public class CopyPart001 {
    public static void main(String[] args) {
        // 您可以通过环境变量获取访问密钥AK/SK，也可以使用其他外部引入方式传入。如果使用硬编码可能会存在泄露风险。
        // 您可以登录访问管理控制台获取访问密钥AK/SK
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        // String securityToken = System.getenv("SECURITY_TOKEN");
        // endpoint填写桶所在的endpoint, 此处以华北-北京四为例，其他地区请按实际情况填写。
        String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
        // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
        //String endPoint = System.getenv("ENDPOINT");
        
        // 创建ObsClient实例
        // 使用永久AK/SK初始化客户端
        ObsClient obsClient = new ObsClient(ak, sk,endPoint);
        // 使用临时AK/SK和SecurityToken初始化客户端
        // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

        try {
            // 分段复制
            final String destBucketName = "destbucketname";
            final String destObjectKey = "destobjectname";
            final String sourceBucketName = "sourcebucketname";
            final String sourceObjectKey = "sourceobjectname";
            // 初始化线程池
            ExecutorService executorService = Executors.newFixedThreadPool(20);
            // 初始化分段上传任务
            InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(destBucketName, destObjectKey);
            InitiateMultipartUploadResult result = obsClient.initiateMultipartUpload(request);
            final String uploadId = result.getUploadId();
            System.out.println("uploadId:" + uploadId + "\n");
            // 获取大对象信息
            ObjectMetadata metadata = obsClient.getObjectMetadata(sourceBucketName, sourceObjectKey);
            // 每段复制100MB
            long partSize = 100 * 1024 * 1024L;
            long objectSize = metadata.getContentLength();
            // 计算需要复制的段数
            long partCount = objectSize % partSize == 0 ? objectSize / partSize : objectSize / partSize + 1;
            final List<PartEtag> partEtags = Collections.synchronizedList(new ArrayList<>());
            // 执行并发复制段
            for (int i = 0; i < partCount; i++) {
                // 复制段起始位置
                final long rangeStart = i * partSize;
                // 复制段结束位置
                final long rangeEnd = (i + 1 == partCount) ? objectSize - 1 : rangeStart + partSize - 1;
                // 分段号
                final int partNumber = i + 1;
                executorService.execute(
                        new Runnable() {
                            @Override
                            public void run() {
                                CopyPartRequest request = new CopyPartRequest();
                                request.setUploadId(uploadId);
                                request.setSourceBucketName(sourceBucketName);
                                request.setSourceObjectKey(sourceObjectKey);
                                request.setDestinationBucketName(destBucketName);
                                request.setDestinationObjectKey(destObjectKey);
                                request.setByteRangeStart(rangeStart);
                                request.setByteRangeEnd(rangeEnd);
                                request.setPartNumber(partNumber);
                                CopyPartResult result;
                                try {
                                    result = obsClient.copyPart(request);
                                    System.out.println("Part#" + partNumber + " done\n");
                                    partEtags.add(new PartEtag(result.getEtag(), result.getPartNumber()));
                                } catch (ObsException e) {
                                    e.printStackTrace();
                                }
                            }
                        });
            }
            // 等待复制完成
            executorService.shutdown();
            while (!executorService.isTerminated()) {
                try {
                    executorService.awaitTermination(5, TimeUnit.SECONDS);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            // 合并段
            CompleteMultipartUploadRequest completeMultipartUploadRequest =
                    new CompleteMultipartUploadRequest(destBucketName, destObjectKey, uploadId, partEtags);
            obsClient.completeMultipartUpload(completeMultipartUploadRequest);
            System.out.println("copyObject successfully");
        } catch (ObsException e) {
            System.out.println("copyObject failed");
            // 请求失败,打印http状态码
            System.out.println("HTTP Code:" + e.getResponseCode());
            // 请求失败,打印服务端错误码
            System.out.println("Error Code:" + e.getErrorCode());
            // 请求失败,打印详细错误信息
            System.out.println("Error Message:" + e.getErrorMessage());
            // 请求失败,打印请求id
            System.out.println("Request ID:" + e.getErrorRequestId());
            System.out.println("Host ID:" + e.getErrorHostId());
            e.printStackTrace();
        } catch (Exception e) {
            System.out.println("copyObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section1710814133913"></a>

-   关于分段上传-初始化分段上传任务的API说明，请参见[初始化上传段任务](https://support.huaweicloud.com/api-obs/obs_04_0098.html)。
-   关于分段上传-上传段的API说明，请参见[上传段](https://support.huaweicloud.com/api-obs/obs_04_0099.html)。
-   关于分段上传-合并段的API说明，请参见[合并段](https://support.huaweicloud.com/api-obs/obs_04_0102.html)。
-   关于分段上传-复制段的API说明，请参见[拷贝段](https://support.huaweicloud.com/api-obs/obs_04_0100.html)。
-   更多关于分段上传的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/ConcurrentCopyPartSample.java)。
-   分段上传过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

