# 上传段\(Java SDK\)<a name="obs_21_0616"></a>

## 功能说明<a name="section57950190"></a>

初始化分段上传任务后，通过分段上传任务的ID，上传段到指定桶中。除了最后一段以外，其他段的大小范围是100KB\~5GB；最后一段的大小范围是0\~5GB。上传的段的编号也有范围限制，其范围是1\~10000。

上传段时，除了指定上传ID，还必须指定段编号。您可以选择1和10000之间的任意段编号。段编号在您正在上传的对象中唯一地标示了段及其位置。如果您使用之前上传的段的同一段编号上传新段，则之前上传的段将被覆盖。无论您何时上传段，OBS都将在其响应中返回ETag标头。对于每个段上传任务，您必须记录每个段编号和ETag值。您在后续的合并请求中需要添加这些值以完成多段上传。

## 接口约束<a name="section336222411129"></a>

-   您必须是桶拥有者或拥有上传段的权限，才能上传段。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:PutObject权限，如果使用桶策略则需授予PutObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   初始化上传段任务并上传一个或多个段之后，您必须合并段或取消多段上传任务，否则碎片会占用您的存储空间并产生一定的存储费用。
-   段任务中的partNumber是唯一的，重复上传相同partNumber的段，后一次上传会覆盖前一次上传内容。多并发上传同一对象的同一partNumber时，服务端遵循Last Write Win策略，但“Last Write”的时间定义为段元数据创建时间。为了保证数据准确性，客户端需要加锁保证同一对象的同一个段上传的并发性。同一对象的不同段并发上传不需要加锁。

## 方法定义<a name="section13922122017430"></a>

obsClient.uploadPart\([UploadPartRequest](#table5791838) [request](#table1210700)\)

## 请求参数说明<a name="section15761413125713"></a>

**表 1**  uploadPart请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|UploadPartRequest|必选|**参数解释：**上传段请求参数，详见UploadPartRequest。|


**表 2**  UploadPartRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|partNumber|int|必选|**参数解释：**段号。**取值范围：**[1,10000]，超出这个范围，OBS将返回400 Bad Request错误。**默认取值：**无|
|uploadId|String|必选|**参数解释：**分段上传任务的ID。任务ID可以通过初始化分段上传任务生成。例如：000001648453845DBB78F2340DD460D8。**约束限制：**长度为32的字符串。**默认取值：**无|
|input|java.io.InputStream|可选|**参数解释：**待上传对象的数据流。**约束限制：**file为null，需要设置input字段不为空；input为null ，需要设置file字段不为空。二者需要选其一。**默认取值：**无|
|file|java.io.File|可选|**参数解释：**待上传对象的文件。**约束限制：**file为null，需要设置input字段不为空；input为null ，需要设置file字段不为空。二者必须选其一。**默认取值：**无|
|offset|long|可选|**参数解释：**源文件中某一分段的起始偏移大小。**取值范围：**非负整数，不大于待上传对象的大小，单位：字节。**默认取值：**0|
|partSize|Long|可选|**参数解释：**当前段的长度。**约束限制：**上传段接口要求除最后一段以外，其他的段大小都要大于100KB。但是上传段接口并不会立即校验上传段的大小（因为不知道是否为最后一段），只有调用合并段接口时才会校验。OBS 3.0的桶支持最小段的大小为100KB，OBS 2.0的桶支持最小段的大小为5MB。**取值范围：**100KB~5GB，单位：字节。**默认取值：**102400字节|
|sseCHeader|SseCHeader|可选|**参数解释：**服务端加密头域。详见SseCHeader。**默认取值：**无|
|attachMd5|boolean|可选|**参数解释：**是否自动计算待上传数据的MD5值。为了保证数据在网络传输过程中不出现错误，可以通过设置UploadPartRequest.setAttachMd5为true来让SDK自动计算每段数据的MD5值（仅在数据源为本地文件时有效），并放到Content-MD5请求头中。OBS服务端会计算上传数据的MD5值与SDK计算的MD5值比较，保证数据完整性。**约束限制：**attachMd5和contentMd5同时使用时，忽略attachMd5字段。**取值范围：**true：自动计算上传数据的MD5值。false：不自动计算上传数据的MD5值。**默认取值：**false|
|contentMd5|String|可选|**参数解释：**待上传段数据的MD5值（经过Base64编码），是上传段数据内容的唯一标识，可以通过该值识别对象内容是否有变化。**约束限制：**attachMd5和contentMd5同时使用时，忽略attachMd5字段。**取值范围：**长度为32的字符串。**默认取值：**无|
|progressListener|ProgressListener|可选|**参数解释：**上传进度，详见ProgressListener。|
|progressInterval|long|可选|**参数解释**上传进度反馈间隔。例子：1024 * 1024L，每上传1MB数据反馈上传进度。**默认取值：**100 * 1024L，单位：字节。|
|autoClose|boolean|可选|**参数解释：**上传完成后，自动关闭数据流。**取值范围：**true：自动关闭数据流。false：不自动关闭数据流。**默认取值：**true|


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


**表 6**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


**表 7**  ProgressListener\(传输进度接口\)成员如下

|**方法名称**|**返回值类型**|**是否必选**|**描述**|
|--|--|--|--|
|progressChanged|void|必选|**参数解释：**获取上传进度，详见progressChanged。**默认取值：**无|


**表 8**  progressChanged参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|status|ProgressStatus|必选|**参数解释：**传输进度数据，详见ProgressStatus。**默认取值：**无|


**表 9**  ProgressStatus方法

|**方法名称**|**返回值类型**|**说明**|
|--|--|--|
|getAverageSpeed()|double|上传平均速率。|
|getInstantaneousSpeed()|double|上传瞬时速率。|
|getTransferPercentage()|int|上传进度百分比。|
|getNewlyTransferredBytes()|long|新增的字节数。|
|getTransferredBytes()|long|已传输的字节数。|
|getTotalBytes()|long|待传输的字节数。|


## 返回结果说明<a name="section116512059959"></a>

**表 10**  UploadPartResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|partNumber|int|**参数解释：**段号。**取值范围：**[1,10000]**默认取值：**无|
|etag|String|**参数解释：**段的Base64编码的128位MD5摘要。ETag是段内容的唯一标识，可以通过该值识别段内容是否有变化。OBS会将服务端收到段数据的ETag值（段数据的MD5值）返回给用户。比如上传段时ETag为A，下载段时ETag为B，则说明段内容发生了变化。ETag只反映变化的内容，而不是其元数据。上传的段或拷贝操作创建的段，都有唯一的ETag。**约束限制：**当对象是服务端加密的对象时，ETag值不是对象的MD5值。**取值范围：**长度为32的字符串。**默认取值：**无|


## 代码示例<a name="section3208164811355"></a>

本示例用于通过obsClient.uploadPart上传段到examplebucket桶中的objectname对象。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.PartEtag;
import com.obs.services.model.UploadPartRequest;
import com.obs.services.model.UploadPartResult;
import java.io.File;
import java.util.ArrayList;
import java.util.List;
public class UploadPart001 {
    public static void main(String[] args) {
        // 您可以通过环境变量获取访问密钥AK/SK，也可以使用其他外部引入方式传入。如果使用硬编码可能会存在泄露风险。
        // 您可以登录访问管理控制台获取访问密钥AK/SK
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        String securityToken = System.getenv("SECURITY_TOKEN");
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
            String uploadId = "upload id from initiateMultipartUpload";
            List<PartEtag> partEtags = new ArrayList<PartEtag>();
            // 上传第一段
            UploadPartRequest request = new UploadPartRequest("examplebucket", "objectname");
            // 设置Upload ID
            request.setUploadId(uploadId);
            // 设置分段号，范围是1~10000，
            request.setPartNumber(1);
            // 设置将要上传的大文件
            request.setFile(new File("localfile"));
            // 设置分段大小
            request.setPartSize(5 * 1024 * 1024L);
            UploadPartResult result = obsClient.uploadPart(request);
            partEtags.add(new PartEtag(result.getEtag(), result.getPartNumber()));
            // 上传第二段
            request = new UploadPartRequest("examplebucket", "objectname");
            // 设置Upload ID
            request.setUploadId(uploadId);
            // 设置分段号
            request.setPartNumber(2);
            // 设置将要上传的大文件
            request.setFile(new File("localfile"));
            // 设置第二段的段偏移量
            request.setOffset(5 * 1024 * 1024L);
            // 设置分段大小
            request.setPartSize(5 * 1024 * 1024L);
            result = obsClient.uploadPart(request);
            partEtags.add(new PartEtag(result.getEtag(), result.getPartNumber()));
            System.out.println("uploadPart successfully");
        } catch (ObsException e) {
            System.out.println("uploadPart failed");
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
            System.out.println("uploadPart failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于分段上传-上传段的API说明，请参见[上传段](https://support.huaweicloud.com/api-obs/obs_04_0099.html)。
-   更多关于分段上传的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/ConcurrentUploadPartSample.java#L276)。
-   分段上传过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

