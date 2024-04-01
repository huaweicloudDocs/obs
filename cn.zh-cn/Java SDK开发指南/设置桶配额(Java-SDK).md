# 设置桶配额\(Java SDK\)<a name="obs_21_0410"></a>

## 功能说明<a name="section6703932"></a>

桶配额是桶容量的上限值。默认情况下，OBS系统和单个桶都没有总数据容量和对象数量的限制。您可以根据需要，为桶设置配额限制来控制桶内允许上传的对象总容量，超过设置的对象容量后，上传对象会失败。例如您为桶设置配额为100G，那么当桶内所有对象的大小总和达到100G后，再上传对象就会因为超过配额导致上传失败。

容量限制只对桶配额设置生效后的对象上传操作有影响， 如果您设置桶配额时，桶配额的数值小于桶中已上传的对象容量，并不会导致桶中已有对象被删除，但该桶后续将不能再上传任何对象。这种情况下只有删除部分已有对象，将已用空间释放到配额限制以下之后才能再次上传新对象。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section10432511122020"></a>

-   桶配额值必须为非负整数，单位为字节。
-   OBS没有提供删除桶配额的接口，您可以将桶配额设置为0来取消配额限制。
-   您必须是桶拥有者或拥有设置桶配额的权限，才能设置桶配额。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:PutBucketQuota权限，如果使用桶策略则需授予PutBucketQuota权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section54232412"></a>

obsClient.setBucketQuota\(String  [bucketName](#table14455523),  [BucketQuota](#table195191356482) [bucketQuota](#table14455523)\)

## 设置桶配额请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|bucketQuota|BucketQuota|必选|**参数解释：**桶的配额信息**约束限制：**详见BucketQuota|


**表 2**  BucketQuota

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketQuota|long|必选|**参数解释：**桶的配额值。**取值范围：**非负整数，单位：字节。**默认取值：**0，表示没有限制桶配额。|


## 返回结果说明<a name="section1155011051819"></a>

**表 3**  返回结果HeaderResponse\(SDK公共响应结果\)各项属性说明

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例<a name="section8517109534"></a>

本示例用于设置exampleBucket桶的桶配额信息。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.BucketQuota;
public class SetBucketQuota001 {
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
            // 示例桶名
            String exampleBucket = "examplebucket";
            // 示例桶配额
            long exampleBucketQuota = 1024 * 1024 * 100L;
            // 设置桶配额为100MB
            BucketQuota quota = new BucketQuota(exampleBucketQuota);
            obsClient.setBucketQuota(exampleBucket, quota);
            System.out.println("SetBucketQuota successfully");
        } catch (ObsException e) {
            System.out.println("SetBucketQuota failed");
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
            System.out.println("SetBucketQuota failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section1424412152448"></a>

-   关于设置桶配额的API说明，请参见[设置桶配额](https://support.huaweicloud.com/api-obs/obs_04_0052.html)。
-   更多关于桶配额的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/BucketOperationsSample.java)。
-   设置桶配额过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   桶和对象相关常见问题请参见[桶和对象相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_1200.html)。

