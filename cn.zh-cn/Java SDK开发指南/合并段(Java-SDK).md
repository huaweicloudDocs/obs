# 合并段\(Java SDK\)<a name="obs_21_0617"></a>

## 功能说明<a name="section40004924"></a>

如果用户上传完所有的段，就可以调用合并段接口，系统将在服务端将用户指定的段合并成一个完整的对象。在执行“合并段”操作以前，用户不能下载已经上传的数据。在合并段时需要将多段上传任务初始化时记录的附加消息头信息拷贝到对象元数据中，其处理过程和普通上传对象带这些消息头的处理过程相同。在并发合并段的情况下，仍然遵循Last Write Win策略，但“Last Write”的时间定义为段任务的初始化时间。

已经上传的段，只要没有取消对应的多段上传任务，都要占用用户的容量配额；对应的多段上传任务“合并段”操作完成后，只有指定的多段数据占用容量配额，用户上传的其他此多段任务对应的段数据如果没有包含在“合并段”操作制定的段列表中，“合并段”完成后系统将删除多余的段数据，且同时释放容量配额。

合并段时，OBS通过按升序的段编号规范化多段来创建对象。如果在初始化上传段任务中提供了任何对象元数据，则OBS会将该元数据与对象相关联。成功完成请求后，段将不再存在。合并段请求必须包括上传ID、段编号和相应的ETag值的列表。OBS响应包括可唯一地识别组合对象数据的ETag。此ETag无需成为对象数据的MD5哈希。

## 接口约束<a name="section1311222191916"></a>

-   您必须是桶拥有者或拥有合并段的权限，才能合并段。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:PutObject权限，如果使用桶策略则需授予PutObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   如果上传了10个段，但合并时只选择了9个段进行合并，那么未被合并的段将会被系统自动删除，未被合并的段删除后不能恢复。在进行合并之前请使用列出已上传的段接口进行查询，仔细核对所有段，确保没有段被遗漏。

## 方法定义<a name="section126324112476"></a>

obsClient.completeMultipartUpload\([CompleteMultipartUploadRequest](#table5791838) [request](#table1210700)\)

## 请求参数说明<a name="section1455817321573"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|CompleteMultipartUploadRequest|必选|**参数解释：**合并段请求参数，详见CompleteMultipartUploadRequest。|


**表 2**  CompleteMultipartUploadRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|partEtag|List<PartEtag>|必选|**参数解释：**待合并的段列表。详情参见PartEtag。|
|uploadId|String|必选|**参数解释：**分段上传任务的ID，例如：000001648453845DBB78F2340DD460D8**取值范围：**长度为32的字符串。**默认取值：**无|
|encodingType|String|可选|**参数解释：**对响应中的对象名objectKey进行指定类型的编码。如果objectKey包含xml 1.0标准不支持的控制字符，可通过设置该参数对响应中的objectKey进行编码。**取值范围：**可选值为url。**默认取值：**无，不设置则不编码。|
|userHeaders|HashMap<String, String>|可选|**参数解释：**用户头域列表。HashMap中第一个String代表用户头域名称，第二个String代表用户头域对应的取值。通过每个SDK设置的用户头域userHeader透传给服务端，使SDK不做处理，让后续使用更灵活。**默认取值：**无|


**表 3**  PartEtag

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|etag|String|是|**参数解释：**段的ETag值。分段的Base64编码的128位MD5摘要。**取值范围：**长度为32的字符串。**默认取值：**无|
|partNumber|Integer|是|**参数解释：**段号。分段号可以是不连续的。**取值范围：**取值范围是[1,10000]的非负整数。**默认取值：**无|


## 返回结果说明<a name="section116512059959"></a>

**表 4**  CompleteMultipartUploadResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|etag|String|**参数解释：**对象的Base64编码的128位MD5摘要。ETag是对象内容的唯一标识，可以通过该值识别对象内容是否有变化。比如上传对象时ETag为A，下载对象时ETag为B，则说明对象内容发生了变化。ETag只反映变化的内容，而不是其元数据。上传的对象或拷贝操作创建的对象，都有唯一的ETag。**约束限制：**当对象是服务端加密的对象时，ETag值不是对象的MD5值，详情可参考合并段。**取值范围：**长度为32的字符串。**默认取值：**无|
|bucketName|String|**参数解释：**合并段所在的桶的桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|**参数解释：**合并段后得到的对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|location|String|**参数解释：**合并段后得到的对象的url。例如：https://example-Bucket.obs.regions.myhuaweicloud.com/example-Object**默认取值：**无|
|versionId|String|**参数解释：**合并段后得到的对象版本号。如果桶的多版本状态为开启，则会返回对象的版本号。**取值范围：**长度为32的字符串。**默认取值：**无|
|objectUrl|String|**参数解释：**合并段后得到的对象的全路径。**默认取值：**无|
|encodingType|String|**参数解释：**用于指定对响应中的对象名objectKey进行指定类型的编码。如果objectKey包含xml 1.0标准不支持的控制字符，可通过设置该参数对响应中的objectKey进行编码。**取值范围：**可选值为url。**默认取值：**无，不设置则不编码。|


## 代码示例<a name="section377495795919"></a>

本示例用于通过接口ObsClient.completeMultipartUpload 利用字段uploadId、partEtags 合并段于桶examplebucket下的objectname对象中：

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.CompleteMultipartUploadRequest;
import com.obs.services.model.PartEtag;
import java.util.ArrayList;
import java.util.List;
public class CompleteMultipartUpload001 {
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
            // 第一段
            PartEtag part1 = new PartEtag();
            part1.setPartNumber(1);
            part1.seteTag("etag1");
            partEtags.add(part1);
            // 第二段
            PartEtag part2 = new PartEtag();
            part2.setPartNumber(2);
            part2.setEtag("etag2");
            partEtags.add(part2);
            CompleteMultipartUploadRequest request =
                    new CompleteMultipartUploadRequest("examplebucket", "objectname", uploadId, partEtags);
            obsClient.completeMultipartUpload(request);
            System.out.println("completeMultipartUpload successfully");
        } catch (ObsException e) {
            System.out.println("CompleteMultipartUpload failed");
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
            System.out.println("completeMultipartUpload failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于分段上传-合并段的API说明，请参见[合并段](https://support.huaweicloud.com/api-obs/obs_04_0102.html)。
-   更多关于分段上传的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/ConcurrentUploadPartSample.java#L276)。
-   分段上传过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

