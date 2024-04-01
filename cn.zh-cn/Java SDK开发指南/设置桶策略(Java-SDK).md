# 设置桶策略\(Java SDK\)<a name="obs_21_0407"></a>

## 功能说明<a name="section61782511"></a>

OBS支持对桶操作进行权限控制，您可以为桶设置访问策略，指定某一个用户对某一个桶是否有权行使某一项指定操作。OBS权限控制的方式有IAM、桶策略和ACL三种，本节将对桶策略接口进行详细介绍，更多权限相关内容可参见《对象存储服务权限配置指南》的[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)章节。

桶策略是作用于所配置的OBS桶及桶内对象的，您可以通过桶策略可为IAM用户或其他账号授权桶及桶内对象的操作权限。允许其他华为云账号访问OBS资源，可以使用桶策略的方式授权对应权限。当不同的桶对于不同的IAM用户有不同的访问控制需求时，需使用桶策略分别授权IAM用户不同的权限。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

除了桶访问权限外，桶的拥有者还可以通过桶策略，提供对桶和桶内对象的集中访问控制。

您可以通过ObsClient.setBucketPolicy设置桶策略。具体格式请参考[Policy格式](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0041.html)，桶策略说明请参考[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，桶策略样例请参考  [桶策略样例](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0004.html)。

更多关于桶策略的内容请参考[桶策略](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0004.html)。

## 接口约束<a name="section16842317279"></a>

-   创建桶和获取桶列表这两个服务级的操作权限，需要通过[IAM权限](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0014.html)配置。
-   由于缓存的存在，配置桶策略后，最长需要等待5分钟策略才能生效。
-   您必须是桶拥有者或拥有设置桶策略的权限，才能设置桶策略。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:PutBucketPolicy权限，如果使用桶策略则需授予PutBucketPolicy权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   请注意，调用设置桶策略接口时，最新一次配置会覆盖原有配置。例如，您已设置了A，B，C 和 D 四个桶策略，现需要添加新的桶策略E，则配置桶策略 E 时，需在原有四个策略的基础上添加策略 E，然后重新上传所有策略。同理，如果您需要删除桶策略 D，则需将策略 D 从原有的 A，B，C 和 D 四个策略中移除，然后重新上传策略 A，B 和C。
-   桶策略内容的具体格式（JSON格式字符串）请参考[对象存储服务API参考](https://support.huaweicloud.com/api-obs/zh-cn_topic_0031051947.html)。
-   以下两种场景无法使用此接口获取桶策略，系统将返回“404 NoSuchBucketPolicy”的错误：
    -   指定桶的策略不存在。
    -   指定桶的标准桶策略为私有且未设置高级桶策略。

## 方法定义<a name="section54232412"></a>

obsClient.setBucketPolicy\(String  [bucketName](#table14455523), String  [policy](#table14455523)\)

## 设置桶策略请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|policy|String|必选|**参数解释：**策略信息，JSON格式的字符串。**约束限制：**Policy中的Resource字段包含的桶名必须和当前设置桶策略的桶名一致。Policy具体格式请参考Policy格式。**默认取值：**无|


## 返回结果说明<a name="section1155011051819"></a>

**表 2**  返回结果HeaderResponse\(SDK公共响应结果\)各项属性说明

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例<a name="section8517109534"></a>

本示例用于设置exampleBucket桶的桶策略。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
public class SetBucketPolicy001 {
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
            // 示例桶策略
            String examplePolicy =
                    "{\"Statement\":[{\"Principal\":\"*\",\"Effect\":\"Allow\",\"Action\":\"ListBucket\",\"Resource\":\""
                            + exampleBucket
                            + "\"}]}";
            obsClient.setBucketPolicy(exampleBucket, examplePolicy);
            System.out.println("SetBucketAcl successfully");
        } catch (ObsException e) {
            System.out.println("SetBucketAcl failed");
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
            System.out.println("SetBucketAcl failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   关于设置桶策略的API说明，请参见[设置桶策略](https://support.huaweicloud.com/api-obs/obs_04_0027.html)。
-   更多关于桶策略的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/BucketOperationsSample.java)。
-   设置桶策略过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   权限相关常见问题请参见[权限相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_1100.html)。

