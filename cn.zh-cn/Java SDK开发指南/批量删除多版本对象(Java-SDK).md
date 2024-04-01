# 批量删除多版本对象\(Java SDK\)<a name="obs_21_1011"></a>

## 功能说明<a name="section52650200"></a>

为节省空间和成本，您可以根据需要删除指定桶中的多个对象。

批量删除对象特性用于将一个桶内的部分对象一次性删除，删除后不可恢复。批量删除对象要求返回结果里包含每个对象的删除结果。OBS的批量删除对象使用同步删除对象的方式，每个对象的删除结果返回给请求用户。

您可以通过ObsClient.deleteObjects接口传入版本号（versionId）删除多版本对象。

## 接口约束<a name="section837115133817"></a>

-   您必须是桶拥有者或拥有批量删除对象的权限，才能批量删除对象。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:DeleteObject权限，如果使用桶策略则需授予DeleteObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   桶没有开启多版本控制功能时，已删除的对象不可恢复，请谨慎操作。
-   批量删除对象一次能接收最大对象数目为1000个，如果超出限制，服务端会返回请求不合法。
-   并发任务分配后，在循环删除多个对象过程中， 如果发生内部错误， 有可能出现数据不一致的情况（某个对象索引数据删除但还有元数据）。

## 方法定义<a name="section192120299303"></a>

obsClient.deleteObjects\([DeleteObjectsRequest](#table421218296302) [deleteRequest](#table72121329103020)\)

## 请求参数说明<a name="section62121529203019"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|deleteRequest|DeleteObjectsRequest|必选|**参数解释：**批量删除对象请求参数，详见DeleteObjectsRequest。|


**表 2**  DeleteObjectsRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|keyAndVersions|List<KeyAndVersion>|必选|**参数解释：**待删除的对象列表，详情参考KeyAndVersion。|
|quiet|boolean|可选|**参数解释：**批量删除对象的响应方式。**取值范围：**false：表示详细模式，返回删除成功和删除失败的所有结果。true：表示简单模式，只返回删除过程中出错的结果。**默认取值：**false|
|encodingType|String|可选|**参数解释：**用于指定对响应中的对象名objectKey进行指定类型的编码。如果objectKey包含xml 1.0标准不支持的控制字符，可通过设置该参数对响应中的objectKey进行编码。**取值范围：**可选值为url。**默认取值：**无，不设置则不编码。|


**表 3**  KeyAndVersion

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|key|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|versionId|String|可选|**参数解释：**对象的版本号，用于删除指定版本号的对象。**取值范围：**长度为32的字符串。**默认取值：**无，如果不设置则默认删除最新版本的对象。|


## 返回结果说明<a name="section32131429193016"></a>

**表 4**  DeleteObjectsResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|deletedObjectResults|List<DeleteObjectResult>|**参数解释：**删除对象后的响应结果，详见DeleteObjectResult。|
|errorResults|List<ErrorResult>|**参数解释：**删除失败的对象列表，详见ErrorResult。|


**表 5**  DeleteObjectResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|versionId|String|**参数解释：**对象的版本号。**取值范围：**长度为32的字符串。**默认取值：**无|
|deleteMarker|boolean|**参数解释：**标识删除的对象是否是删除标记。**取值范围：**true：是删除标记。false：不是删除标记。**默认取值：**false|
|objectKey|String|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|


**表 6**  ErrorResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|versionId|String|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|errorCode|String|**参数解释**：删除失败的错误码。可参考OBS错误码。|
|objectKey|String|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|message|String|**参数解释**：删除失败的错误原因。可参考OBS错误码。|


## 代码示例<a name="section179775814719"></a>

您可以通过ObsClient.deleteObjects接口传入每个待删除对象的版本号（versionId）为examplebucket桶批量删除多版本对象，示例代码如下：

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.DeleteObjectsRequest;
import com.obs.services.model.DeleteObjectsResult;
import com.obs.services.model.KeyAndVersion;
import java.util.ArrayList;
import java.util.List;
public class DeleteObjects001 {
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
            // 批量删除多版本对象
            DeleteObjectsRequest request = new DeleteObjectsRequest("examplebucket");
            request.setQuiet(false);
            List<KeyAndVersion> toDelete = new ArrayList<KeyAndVersion>();
            toDelete.add(new KeyAndVersion("objectname1", "versionid1"));
            toDelete.add(new KeyAndVersion("objectname2", "versionid2"));
            toDelete.add(new KeyAndVersion("objectname3", "versionid3"));
            request.setKeyAndVersions(toDelete.toArray(new KeyAndVersion[toDelete.size()]));
            DeleteObjectsResult result = obsClient.deleteObjects(request);
            System.out.println("deleteObjects successfully");
            System.out.println("getDeletedObjectResults:" + result.getDeletedObjectResults());
            System.out.println("getErrorResults:" + result.getErrorResults());
        } catch (ObsException e) {
            System.out.println("deleteObjects failed");
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
            System.out.println("deleteObjects failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于批量删除对象的API说明，请参见[批量删除对象](https://support.huaweicloud.com/api-obs/obs_04_0086.html)。
-   更多关于删除对象的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/ListVersionsSample.java)。
-   删除对象过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

