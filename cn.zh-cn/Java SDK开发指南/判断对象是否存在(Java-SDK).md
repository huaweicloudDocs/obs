# 判断对象是否存在\(Java SDK\)<a name="obs_21_0807"></a>

## 功能说明<a name="section59325057"></a>

判断对象是否存在，返回的结果中HTTP状态码为200表明对象存在，否则返回404表明对象或桶不存在。

## 接口约束<a name="section76593615308"></a>

-   您必须是桶拥有者或拥有列举桶内对象的权限，才能判断判断对象是否存在。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:ListBucket权限，如果使用桶策略则需授予ListBucket权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section54232412"></a>

doesObjectExist\(final  [GetObjectMetadataRequest](#obs_21_0801_table14455523) [request](#obs_21_0801_table1210700)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|GetObjectMetadataRequest|必选|**参数解释：**设置对象属性请求参数，详见GetObjectMetadataRequest。|


**表 2**  GetObjectMetadataRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|必选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|versionId|String|可选|**参数解释：**对象的版本号。**取值范围：**长度为32的字符串。**默认取值：**无|
|userHeaders|HashMap<String, String>|可选|**参数解释：**用户头域列表。HashMap中第一个String代表用户头域名称，第二个String代表用户头域名称对应的取值。通过每个SDK设置的用户头域userHeader透传给服务端，使SDK不做处理，让后续使用更灵活。**取值范围：**长度为32的字符串。**默认取值：**无|
|encodeHeaders|boolean|可选|**参数解释：**设置对象元数据接口允许指定是否编解码http头域。**取值范围：**true：对象元数据接口允许进行编解码http头域。false：对象元数据接口允许不进行编解码http头域。**默认取值：**默认为true，默认会进行编解码。|
|sseHeader|SseCHeader|可选|**参数解释：**服务端解密头信息。详见SseCHeader。|


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


## 返回结果说明<a name="section1155011051819"></a>

**表 6**  返回结果如下

|**方法名称**|**返回值类型**|**说明**|
|--|--|--|
|doesObjectExist(final GetObjectMetadataRequest  request)|boolean|用于判断桶中相关对象是否存在。|


## 代码示例<a name="section12628194364710"></a>

本示例用于判断examplebucket桶里面objectname对象是否存在。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
public class DoesObjectExist001 {
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
            // 判断指定的对象是否存在
            System.out.println(obsClient.doesObjectExist("examplebucket", "objectname") ? "exists!" : "does not exist!");
            System.out.println("doesObjectExist successfully");
        } catch (ObsException e) {
            System.out.println("doesObjectExist failed");
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
            System.out.println("doesObjectExist failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section2195102712454"></a>

-   判断对象是否存在过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

