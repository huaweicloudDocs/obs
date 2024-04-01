# 获取桶策略\(Java SDK\)<a name="obs_21_0413"></a>

## 功能介绍<a name="section98621714142118"></a>

OBS支持对桶操作进行权限控制，您可以为桶设置访问策略，指定某一个用户对某一个桶是否有权行使某一项指定操作。OBS权限控制的方式有IAM、桶策略和ACL三种，本节将对桶策略接口进行详细介绍，更多权限相关内容可参见《对象存储服务权限配置指南》的[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)章节。

调用获取桶策略接口，您可获取指定桶的桶策略。

## 接口约束<a name="section10947231102816"></a>

-   以下两种场景无法使用此接口获取桶策略，系统将返回“404 NoSuchBucketPolicy”的错误：
    -   指定桶的策略不存在。
    -   指定桶的标准桶策略为私有且未设置高级桶策略。

-   您必须是桶拥有者或拥有获取桶策略的权限，才能获取桶策略。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:GetBucketPolicy权限，如果使用桶策略则需授予GetBucketPolicy权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section46703582"></a>

obsClient.getBucketPolicy\(String  [bucketName](#table25490811)\)

## 获取桶策略请求参数说明<a name="section17679057"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|


## 返回结果说明<a name="section11714819134717"></a>

**表 2**  返回结果列表

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|policy|String|**参数解释：**策略信息，JSON格式的字符串。**约束限制：**Policy中的Resource字段包含的桶名必须和当前设置桶策略的桶名一致。Policy具体格式请参考Policy格式。**默认取值：**无|


## 代码示例<a name="section293195113615"></a>

本示例用于获取exampleBucket桶的桶策略。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
public class GetBucketPolicy001 {
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
            String policy = obsClient.getBucketPolicy(exampleBucket);
            System.out.println("\t" + policy);
        } catch (ObsException e) {
            System.out.println("GetBucketAcl failed");
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
            System.out.println("GetBucketAcl failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section261317194815"></a>

-   关于获取桶策略的API说明，请参见[获取桶策略](https://support.huaweicloud.com/api-obs/obs_04_0028.html)。
-   更多关于桶策略的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/BucketOperationsSample.java)。
-   设置桶策略过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   权限相关常见问题请参见[权限相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_1100.html)。

