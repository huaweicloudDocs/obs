# 取消分段上传任务\(Java SDK\)<a name="obs_21_0619"></a>

## 功能说明<a name="section11088383"></a>

通过分段上传任务的ID，取消指定桶中的分段上传任务。

您可以选择取消多段上传任务，取消多段上传任务之后无法再次使用该上传ID上传任何段。然后，OBS将释放被取消的多段上传任务中的每个段数据的所有存储。如果有多段上传已在进行中，即使您已执行中止操作，它们仍可以上传成功或失败。如果要释放所有分段使用的所有存储，必须在完成所有多段上传后再取消多段上传任务。

## 接口约束<a name="section2647246154912"></a>

-   您必须是桶拥有者或拥有取消分段上传任务的权限，才能取消分段上传任务。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:AbortMultipartUpload权限，如果使用桶策略则需授予AbortMultipartUpload权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section25743851"></a>

obsClient.abortMultipartUpload\([AbortMultipartUploadRequest](#table463252217813) [request](#table9136105616812)\)

## 请求参数<a name="section76654495217"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|AbortMultipartUploadRequest|必选|**参数解释：**取消分段请求参数，详见AbortMultipartUploadRequest。|


**表 2**  AbortMultipartUploadRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|桶名。**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|uploadId|String|必选|**参数解释：**分段上传任务的ID，例如：000001648453845DBB78F2340DD460D8**取值范围：**长度为32的字符串。**默认取值：**无|


## 返回结果说明<a name="section116512059959"></a>

**表 3**  返回结果HeaderResponse\(SDK公共响应结果\)各项属性说明

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例<a name="section129258587127"></a>

通过ObsClient.abortMultipartUpload利用初始化多段上传时获取的uploadId，取消对examplebucket桶中的objectname对象分段上传任务。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.AbortMultipartUploadRequest;
public class AbortMultipartUpload001 {
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
            // 取消分段上传任务请求
            AbortMultipartUploadRequest request = new AbortMultipartUploadRequest("examplebucket", "objectname", uploadId);
            // 取消分段上传任务接口
            obsClient.abortMultipartUpload(request);
            System.out.println("AbortMultipartUpload successfully");
        } catch (ObsException e) {
            System.out.println("AbortMultipartUpload failed");
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
            System.out.println("AbortMultipartUpload failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于分段上传-取消分段上传任务的API说明，请参见[取消多段上传任务](https://support.huaweicloud.com/api-obs/obs_04_0103.html)。
-   更多关于分段上传的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/ConcurrentUploadPartSample.java#L276)。
-   分段上传过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

