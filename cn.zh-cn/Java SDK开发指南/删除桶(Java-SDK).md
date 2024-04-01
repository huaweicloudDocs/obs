# 删除桶\(Java SDK\)<a name="obs_21_0403"></a>

## 功能说明<a name="section18068130"></a>

桶为空时，用户可以删除桶，以免占用桶数量配额。删除桶后需要等待30分钟才能创建同名桶。

>![](public_sys-resources/icon-note.gif) **说明：** 
>华为云无法恢复用户主动删除的OBS数据。因此调用接口删除桶后，桶相关数据无法恢复，请谨慎操作。

## 接口约束<a name="section089717141092"></a>

-   待删除的桶必须为空，桶为空包含两方面含义：
    -   桶内没有任何对象，没有对象的任何历史版本，没有对象的删除标记（删除标记也视作一个历史版本）。
    -   桶内没有任何未合并的多段上传任务，即桶内不存在碎片。

-   您必须是桶拥有者或拥有删除桶的权限，才能删除桶。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:DeleteBucket权限，如果使用桶策略则需授予DeleteBucket权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   如果桶不为空（包含对象或分段上传碎片），则该桶无法被删除。
-   删除桶不是“幂等”操作，删除不存在的桶会报错。

## 方法定义<a name="section54232412"></a>

obsClient.deleteBucket\(String  [bucketName](#table1210700)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|


## 返回结果<a name="section1155011051819"></a>

**表 2**  返回结果HeaderResponse\(SDK公共响应结果\)各项属性说明

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例<a name="section165812810487"></a>

本示例用于删除桶名为exampleBucket的桶。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HeaderResponse;
public class DeleteBucket001 {
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
            //示例桶名
            String exampleBucket = "examplebucket";
            // 删除桶
            HeaderResponse response = obsClient.deleteBucket(exampleBucket);
            System.out.println("DeleteBucket successfully");
            System.out.println("StatusCode:"+response.getStatusCode());
            System.out.println("RequestId:"+response.getRequestId());
        } catch (ObsException e) {
            System.out.println("DeleteBucket failed");
            // 请求失败,打印http状态码
            System.out.println("HTTP Code:" + e.getResponseCode());
            // 请求失败,打印服务端错误码
            System.out.println("Error Code:" + e.getErrorCode());
            // 请求失败,打印详细错误信息
            System.out.println("Error Message: " + e.getErrorMessage());
            // 请求失败,打印请求id
            System.out.println("Request ID:" + e.getErrorRequestId());
            System.out.println("Host ID:" + e.getErrorHostId());
        } catch (Exception e) {
            System.out.println("DeleteBucket failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   如何删除桶内对象和历史版本，请参见[删除对象](https://support.huaweicloud.com/ugobs-obs/obs_41_0028.html)。
-   如何清理碎片，请参见[清理碎片](https://support.huaweicloud.com/ugobs-obs/obs_41_0030.html)。
-   您可以使用[列举桶内对象](https://support.huaweicloud.com/ugobs-obs/obs_41_0019.html)和[列举多段上传任务](https://support.huaweicloud.com/api-obs/obs_04_0097.html)来确认桶是否为空。
-   关于删除桶的API说明，请参见[删除桶](https://support.huaweicloud.com/api-obs/obs_04_0025.html)。
-   更多关于删除桶的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/BucketOperationsSample.java)。
-   删除桶过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   删除桶常见问题请参见[删除桶失败](https://support.huaweicloud.com/obs_faq/obs_faq_0064.html)。

