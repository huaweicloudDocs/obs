# 设置跨域资源共享规则\(Java SDK\)<a name="obs_21_1402"></a>

## 功能介绍<a name="section34091413"></a>

跨域资源共享（Cross Origin Resource Sharing，CORS）是由W3C标准化组织提出的一种网络浏览器的规范机制，定义了一个域中加载的客户端Web应用程序与另一个域中的资源交互的方式。而在通常的网页请求中，由于同源安全策略（Same Origin Policy，SOP）的存在，不同域之间的网站脚本和内容是无法进行交互的。OBS支持CORS规范，允许跨域请求访问OBS中的资源。

您可以通过ObsClient.setBucketCors设置桶的跨域规则，如果原规则存在则覆盖原规则。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section326152964516"></a>

-   您必须是桶拥有者或拥有设置桶的CORS配置的权限，才能设置桶的CORS配置。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:PutBucketCORS权限，如果使用桶策略则需授予PutBucketCORS权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section54232412"></a>

obsclient.setBucketCors\(final  [SetBucketCorsRequest](#table14455523) [request](#table1210700)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|SetBucketCorsRequest|必选|设置跨域规则请求参数，详见SetBucketCorsRequest。|


**表 2**  SetBucketCorsRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|bucketCors|BucketCors|必选|**参数解释：**桶的CORS规则列表。详见BucketCors。|


**表 3**  BucketCors

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|rules|List<BucketCorsRule>|必选|**参数解释：**桶的CORS规则列表。详见BucketCorsRule。|


**表 4**  BucketCorsRule

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|id|String|可选|**参数解释：**CORS规则ID**取值范围：**长度大于0且不超过255的字符串。**默认取值：**无|
|allowedMethod|List<String>|必选|**参数解释：**指定允许的跨域请求HTTP方法，即桶和对象的几种操作类型。**取值范围：**支持以下HTTP方法：GETPUTHEADPOSTDELETE**默认取值：**无|
|allowedOrigin|List<String>|必选|**参数解释：**指定允许的跨域请求的来源，即允许来自该域名下的请求访问该桶。**约束限制：**表示域名的字符串，每个匹配规则允许使用最多一个“*”通配符。例如：https://*.vbs.example.com。**默认取值：**无|
|allowedHeader|List<String>|可选|**参数解释：**指定允许的跨域请求的头域。只有匹配上允许的头域中的配置，才被视为是合法的CORS请求。**约束限制：**最多可填写一个“*”通配符，不支持&、:、<、空格以及中文字符。**默认取值：**无|
|maxAgeSeconds|int|可选|**参数解释：**CORS规则允许客户端可以对跨域请求返回结果的缓存时间。**约束限制：**每个BucketCorsRule可以包含至多一个maxAgeSeconds。**取值范围：**不小于0的整型数，单位：秒。**默认取值：**100|
|exposeHeader|List<String>|可选|**参数解释：**CORS规则允许响应中可返回的附加头域，给客户端提供额外的信息。默认情况下浏览器只能访问以下头域：Content-Length、Content-Type，如果需要访问其他头域，需要在附加头域中配置。**约束限制：**不支持*、&、:、<、空格以及中文字符。**默认取值：**无|


## 返回结果说明<a name="section1155011051819"></a>

**表 5**  返回结果HeaderResponse\(SDK公共响应结果\)各项属性说明

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例<a name="section510813419506"></a>

本示例用于配置examplebucket桶的CORS规则。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.BucketCors;
import com.obs.services.model.BucketCorsRule;
import com.obs.services.model.DeleteObjectsRequest;
import com.obs.services.model.DeleteObjectsResult;
import com.obs.services.model.KeyAndVersion;
import java.util.ArrayList;
import java.util.List;
public class SetBucketCors001 {
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
            // 设置跨域规则
            BucketCors cors = new BucketCors();
            List<BucketCorsRule> rules = new ArrayList<BucketCorsRule>();
            BucketCorsRule rule = new BucketCorsRule();
            ArrayList<String> allowedOrigin = new ArrayList<String>();
            // 指定允许跨域请求的来源
            allowedOrigin.add( "http://www.a.com");
            allowedOrigin.add( "http://www.b.com");
            rule.setAllowedOrigin(allowedOrigin);
            ArrayList<String> allowedMethod = new ArrayList<String>();
            // 指定允许的跨域请求方法(GET/PUT/DELETE/POST/HEAD)
            allowedMethod.add("GET");
            allowedMethod.add("HEAD");
            allowedMethod.add("PUT");
            rule.setAllowedMethod(allowedMethod);
            ArrayList<String> allowedHeader = new ArrayList<String>();
            // 控制在OPTIONS预取指令中Access-Control-Request-Headers头中指定的header是否被允许使用
            allowedHeader.add("x-obs-header");
            rule.setAllowedHeader(allowedHeader);
            ArrayList<String> exposeHeader = new ArrayList<String>();
            // 指定允许用户从应用程序中访问的header
            exposeHeader.add("x-obs-expose-header");
            rule.setExposeHeader(exposeHeader);
            // 指定浏览器对特定资源的预取(OPTIONS)请求返回结果的缓存时间,单位为秒
            rule.setMaxAgeSecond(10);
            rules.add(rule);
            cors.setRules(rules);
            obsClient.setBucketCors("examplebucket", cors);
            System.out.println("setBucketCors successfully");
        } catch (ObsException e) {
            System.out.println("setBucketCors failed");
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
            System.out.println("setBucketCors failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   关于设置桶的跨域规则的API说明，请参见[设置桶的CORS配置](https://support.huaweicloud.com/api-obs/obs_04_0074.html)。
-   更多关于设置桶的跨域规则的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/BucketOperationsSample.java)。
-   设置桶的跨域规则过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

