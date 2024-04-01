# 获取桶多版本状态\(Java SDK\)<a name="obs_21_1003"></a>

## 功能说明<a name="section119531911164718"></a>

OBS支持多版本控制，您可以在一个桶中保留对象的多个版本，使您更方便地检索和还原各个版本，在意外操作或应用程序故障时快速恢复数据。更多多版本相关信息请参见[多版本控制](https://support.huaweicloud.com/ugobs-obs/obs_41_0047.html)。

调用获取桶的多版本状态接口，您可以获取指定桶的多版本状态。

## 接口约束<a name="section4632132111319"></a>

-   您必须是桶拥有者或拥有获取桶的多版本状态的权限，才能获取桶的多版本状态。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:GetBucketVersioning权限，如果使用桶策略则需授予GetBucketVersioning权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section54232412"></a>

obsClient.getBucketVersioning\(final  [BaseBucketRequest](#table13982202) [request](#table1210700)\)

## 请求参数说明<a name="section5908907"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|BaseBucketRequest|必选|**参数解释：**查看桶多版本状态请求参数，详见BaseBucketRequest。|


**表 2**  BaseBucketRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|


## 返回结果说明<a name="section1155011051819"></a>

**表 3**  BucketVersioningConfiguration

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|status|VersioningStatusEnum|**参数解释：**桶的多版本状态。**取值范围：**详见VersioningStatusEnum。|


**表 4**  VersioningStatusEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|SUSPENDED|Suspended|暂停多版本。|
|ENABLED|Enabled|开启多版本。|


## 代码示例<a name="section062175653812"></a>

以下代码展示了如何查看examplebucket桶的多版本状态。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.BucketVersioningConfiguration;
public class GetBucketVersioning001 {
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
            // 查看桶多版本状态
            BucketVersioningConfiguration status = obsClient.getBucketVersioning("examplebucket");
            System.out.println("getBucketVersioning successfully");
            System.out.println("getVersioningStatus:" + status.getVersioningStatus());
        } catch (ObsException e) {
            System.out.println("getBucketVersioning failed");
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
            System.out.println("getBucketVersioning failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   关于查看桶多版本状态的API说明，请参见[获取桶的多版本状态](https://support.huaweicloud.com/api-obs/obs_04_0038.html)。
-   更多关于查看桶多版本状态的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/BucketOperationsSample.java)。
-   查看桶多版本状态过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   多版本控制相关问题请参见[多版本控制相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_0800.html)。

