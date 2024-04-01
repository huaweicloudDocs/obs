# 获取桶元数据\(Java SDK\)<a name="obs_21_0405"></a>

## 功能说明<a name="section11921553"></a>

调用获取桶元数据接口，可获取指定桶的相关信息，包括指定桶的存储类别、区域位置、跨域资源共享（CORS）规则、冗余策略等信息。

## 接口约束<a name="section630643201420"></a>

-   您必须是桶拥有者或拥有获取桶元数据的权限，才能获取桶元数据。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:HeadBucket权限，如果使用桶策略则需授予HeadBucket权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   BucketMetadataInfoResult.getAllowMethods等方法的值参见桶的[跨域资源共享](跨域资源共享简介(Java-SDK).md)（CORS）配置。

## 方法定义<a name="section54232412"></a>

obsClient.getBucketMetadata\([BucketMetadataInfoRequest](#table14455523) [request](#table1210700)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|BucketMetadataInfoRequest|必选|**参数解释：**获取桶元数据请求参数，详BucketMetadataInfoRequest。|


**表 2**  BucketMetadataInfoRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|origin|String|可选|**参数解释：**预请求指定的跨域请求origin（通常为域名）。**约束限制：**允许多条匹配规则，以回车换行为间隔。每个匹配规则允许使用最多一个“*”通配符。**默认取值：**无|
|requestHeaders|List<String>|可选|**参数解释：**跨域请求可以使用的HTTP头域。只有匹配上允许的头域中的配置，才被视为是合法的CORS请求。**约束限制：**允许的头域可设置多个，多个头域之间换行隔开，每行最多可填写一个*符号，不支持&、:、<、空格以及中文字符。**默认取值：**无|


## 返回结果说明<a name="section1155011051819"></a>

**表 3**  BucketMetadataInfoResult

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|
|location|String|**参数解释：**桶所在的区域。**约束限制：**该参数定义了桶将会被创建在哪个区域，如果使用的终端节点是obs.myhuaweicloud.com，可以不携带此参数；如果使用的终端节点不是obs.myhuaweicloud.com，则必须携带此参数。**取值范围：**当前有效的OBS区域和终端节点的更多信息，请参考地区和终端节点。终端节点即调用API的请求地址，不同服务不同区域的终端节点不同，您可以向企业管理员获取区域和终端节点信息。**默认取值：**终端节点为obs.myhuaweicloud.com且用户未设定区域时，默认为华北-北京一（cn-north-1）。|
|obsVersion|String|**参数解释：**桶所在的OBS服务版本号。**取值范围：**“3.0”表示最新版本的桶。“--”表示老版本的桶。**默认取值：**无|
|storageClass|StorageClassEnum|**参数解释：**创桶时可指定的桶的存储类别。**取值范围：**可选择的访问策略选项参见StorageClassEnum。**默认取值：**STANDARD，即标准存储类别。|
|allowOrigin|String|**参数解释：**如果请求中的Origin满足桶的CORS规则，则返回CORS规则中的AllowedOrigin。**约束限制：**允许多条匹配规则，以回车换行为间隔。每个匹配规则允许使用最多一个“*”通配符。**默认取值：**无|
|allowHeaders|List<String>|**参数解释：**如果请求中的RequestHeader满足桶的CORS规则，则返回CORS规则中的AllowedHeader。**约束限制：**允许的头域可设置多个，多个头域之间换行隔开，每行最多可填写一个*符号，不支持&、:、<、空格以及中文字符。**默认取值：**无|
|allowMethods|List<String>|**参数解释：**指定允许的跨域请求HTTP方法，即桶和对象的几种操作类型。**取值范围：**支持以下HTTP方法：GETPUTHEADPOSTDELETE**默认取值：**无|
|exposeHeaders|List<String>|**参数解释：**CORS规则允许响应中可返回的附加头域，给客户端提供额外的信息。默认情况下浏览器只能访问以下头域：Content-Length、Content-Type，如果需要访问其他头域，需要在附加头域中配置。**约束限制：**不支持*、&、:、<、空格以及中文字符。**默认取值：**无|
|maxAge|int|**参数解释：**请求来源的客户端可以对跨域请求返回结果的缓存时间。**约束限制：**每个CORSRule可以包含至多一个maxAge。**取值范围：**大于0的整型数，单位：秒。**默认取值：**100|
|epid|String|**参数解释：**创桶时可指定的企业项目ID，开通企业项目的用户可以从企业项目服务获取。**约束限制：**Epid格式为uuid，默认项目传“0”或者不带该头域，未开通企业项目的用户可以不带该头域。示例：9892d768-2d13-450f-aac7-ed0e44c2585f**取值范围：**获取方式参见如何获取企业项目ID 。**默认取值：**无|
|bucketType|BucketTypeEnum|**参数解释：**创建的桶类型。**取值范围：**详见BucketTypeEnum。**默认取值：**OBJECT，即对象桶。|
|availableZone|AvailableZoneEnum|**参数解释：**桶的数据冗余存储策略属性，反映数据是单AZ存储还是多AZ存储。详见AvailableZoneEnum**约束限制：**取值为3az，表示数据冗余存储在同一区域的多个可用区。不携带此头域表示为单az存储，仅使用1个可用区存储。**默认取值：**无|


**表 4**  BucketTypeEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|OBJECT|OBJECT|对象桶|
|PFS|POSIX|并行文件系统|


**表 5**  AvailableZoneEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|MULTI_AZ|3az|多az类型|


**表 6**  StorageClassEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|STANDARD|STANDARD|标准存储。|
|WARM|WARM|低频访问存储。|
|COLD|COLD|归档存储。|


## 代码示例<a name="section527415211592"></a>

本示例用于获取examplebucke桶的元数据信息，指定的跨域请求origin为“http://www.exampleorigin.com”。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.BucketMetadataInfoRequest;
import com.obs.services.model.BucketMetadataInfoResult;
public class GetBucketMetadata001 {
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
        // String endPoint = System.getenv("ENDPOINT");

        // 创建ObsClient实例
        // 使用永久AK/SK初始化客户端
        ObsClient obsClient = new ObsClient(ak, sk,endPoint);
        // 使用临时AK/SK和SecurityToken初始化客户端
        // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

        try {
            //示例桶名
            String exampleBucket = "examplebucket";
            //示例Origin
            String exampleOrigin = "http://www.exampleorigin.com";
            BucketMetadataInfoRequest request = new BucketMetadataInfoRequest(exampleBucket);
            //只有在涉及 cors 时才需要 setOrigin
            request.setOrigin(exampleOrigin);
            // 获取桶元数据
            BucketMetadataInfoResult result = obsClient.getBucketMetadata(request);
            System.out.println("GetBucketMetadata successfully");
            System.out.println("GetBucketType:" + result.getBucketType());
            System.out.println("GetLocation:" + result.getLocation());
            System.out.println("GetBucketStorageClass:" + result.getBucketStorageClass());
            System.out.println("GetObsVersion:" + result.getObsVersion());
            System.out.println("GetAllowOrigin:" + result.getAllowOrigin());
            System.out.println("GetMaxAge:" + result.getMaxAge());
            System.out.println("GetAllowHeaders:" + result.getAllowHeaders());
            System.out.println("GetAllowMethods:" + result.getAllowMethods());
            System.out.println("GetExposeHeaders:" + result.getExposeHeaders());
        } catch (ObsException e) {
            System.out.println("GetBucketMetadata failed");
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
            System.out.println("GetBucketMetadata failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   关于获取桶元数据的API说明，请参见[获取桶元数据](https://support.huaweicloud.com/api-obs/obs_04_0023.html)。
-   更多关于获取桶元数据的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/BucketOperationsSample.java)。
-   获取桶元数据过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   桶和对象相关常见问题请参见[桶和对象相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_1200.html)。

