# 修改写对象\(Java SDK\)<a name="obs_21_0503"></a>

## 功能说明<a name="section20005910"></a>

将指定并行文件系统内的一个对象从指定位置起修改为其他内容。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section15696348102310"></a>

-   您必须是并行文件系统拥有者或拥有修改写对象的权限，才能修改写对象。建议使用IAM或策略进行授权，如果使用IAM则需授予obs:bucket:PutObject权限，如果使用策略则需授予PutObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   目前接口仅在并行文件系统支持，普通对象并行文件系统不支持，如何创建并行文件系统请参考[创建并行文件系统\(Java SDK\)](创建并行文件系统(Java-SDK).md)。

## 方法定义<a name="section54232412"></a>

obsClient.modifyObject\([ModifyObjectRequest](#table14455523) [request](#table1210700)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|ModifyObjectRequest|必选|**参数解释：**修改写对象请求参数，详见ModifyObjectRequest。|


**表 2**  ModifyObjectRequest

|**参数名称**|**参数类型**|**是否可选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|position|long|必选|**参数解释：**修改写操作的位置。**取值范围：**不小于0的长整型。单位：字节。**默认取值：**无|
|input|InputStream|可选|**参数解释：**待上传对象的数据流。**默认取值：**无|
|file|File|可选|**参数解释：**待上传的本地文件。**默认取值：**无|
|encodeHeaders|boolean|可选|**参数解释：**是否开启OBS对请求头域的自动编码。由于HTTP编码规范限制，无法发送非ASCII码字符，SDK会在发送请求时对您头域中的**中文汉字**进行url编码，发送编码后数据。如您设置的值content-disposition为“attachment; filename="中文.txt"”，则对象元数据中存储的信息为“attachment; filename="%E4%B8%AD%E6%96%87.txt"”。使用浏览器访问时浏览器将会自动解码。**取值范围：**true：启用SDK编码。false：不启用SDK编码。**默认取值：**true|


## 返回结果说明<a name="section1155011051819"></a>

**表 3**  ModifyObjectResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例<a name="section1411113101371"></a>

本示例用于指定位置修改examplebucket并行文件系统中objectname对象的内容。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ModifyObjectRequest;
import com.obs.services.model.ModifyObjectResult;
import java.io.ByteArrayInputStream;
public class ModifyObject001 {
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
            // 第一次上传
            ModifyObjectRequest request = new ModifyObjectRequest();
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname");
            request.setPosition(0);
            request.setInput(new ByteArrayInputStream("HELLO OBS FIRST".getBytes()));
            ModifyObjectResult result = obsClient.modifyObject(request);
            // 第二次修改写
            request.setPosition(0);
            request.setInput(new ByteArrayInputStream("hello obs second".getBytes()));
            result = obsClient.modifyObject(request);
            System.out.println("modifyObject successfully");
            System.out.println("HTTP Code: " + result.getStatusCode());
        } catch (ObsException e) {
            System.out.println("modifyObject failed");
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
            System.out.println("modifyObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于修改写对象的API说明，请参见[修改写对象](https://support.huaweicloud.com/api-obs/obs_04_0092.html)。
-   更多关于修改写对象的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/PFSBucketAndObjectOperationSample.java)。
-   修改写对象过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   修改写对象常见问题请参见[我可以修改对象名称吗？](https://support.huaweicloud.com/obs_faq/obs_faq_1000.html)。

