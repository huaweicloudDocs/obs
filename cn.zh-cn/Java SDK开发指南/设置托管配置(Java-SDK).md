# 设置托管配置\(Java SDK\)<a name="obs_21_1603"></a>

## 功能介绍<a name="section63661202"></a>

OBS允许在桶内保存静态的网页资源，如.html网页文件、flash文件、音视频文件等，当客户端通过桶的Website接入点访问这些对象资源时，浏览器可以直接解析出这些支持的网页资源，呈现给最终用户。典型的应用场景有：

-   重定向所有的请求到另外一个站点。
-   设定特定的重定向规则来重定向特定的请求。

调用设置桶的网站配置接口，您可以为指定桶设置网站配置信息。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section326152964516"></a>

-   尽量避免目标桶名中带有“.”，否则通过HTTPS访问时可能出现客户端校验证书出错。
-   设置桶的网站配置请求消息体的上限是10KB。
-   您必须是桶拥有者或拥有设置桶的网站配置的权限，才能设置桶的网站配置。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:bucket:PutBucketWebsite权限，如果使用桶策略则需授予PutBucketWebsite权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[自定义创建桶策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0123.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section54232412"></a>

obsClient.setBucketWebsite\(final  [SetBucketWebsiteRequest](#table14455523) [request](#table1210700)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|SetBucketWebsiteRequest|必选|**参数解释：**设置托管配置请求参数，详见SetBucketWebsiteRequest。|


**表 2**  SetBucketWebsiteRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|必选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**取值范围：**长度为3～63个字符。|
|websiteConfig|WebsiteConfiguration|必选|**参数解释：**静态网站设置托管配置信息，详见WebsiteConfiguration。|


**表 3**  WebsiteConfiguration

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|suffix|String|可选|**参数解释：**该字段被追加在对文件夹的请求的末尾（例如：suffix参数设置为“index.html”，请求的是“samplebucket/images/”，返回的数据将是“samplebucket”桶内名为“images/index.html”的对象的内容）。**约束限制：**key、suffix和routeRules必须配套使用，且与redirectAllRequestsTo互斥。当设置了这三个字段时，不能设置redirectAllRequestsTo；反之，当设置了redirectAllRequestsTo时，不能设置key、suffix和routeRules。当key、suffix和routeRules三个字段一起使用时，routeRules可为空。设置key、suffix和routeRules时不能全为空。**取值范围：**该字段不能为空或者包含“/”字符。**默认取值：**无|
|key|String|可选|**参数解释：**当4XX错误出现时使用的对象的名称。这个元素指定当错误出现时返回的页面。**约束限制：**key、suffix和routeRules必须配套使用，且与redirectAllRequestsTo互斥。当设置了这三个字段时，不能设置redirectAllRequestsTo；反之，当设置了redirectAllRequestsTo时，不能设置key、suffix和routeRules。当key、suffix和routeRules三个字段一起使用时，routeRules可为空。设置key、suffix和routeRules时不能全为空。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|routeRules|List<RouteRule>|可选|**参数解释：**请求重定向规则列表，详见RouteRule。**约束限制：**key、suffix和routeRules必须配套使用，且与redirectAllRequestsTo互斥。当设置了这三个字段时，不能设置redirectAllRequestsTo；反之，当设置了redirectAllRequestsTo时，不能设置key、suffix和routeRules。当key、suffix和routeRules三个字段一起使用时，routeRules可为空。设置key、suffix和routeRules时不能全为空。**默认取值：**无|
|redirectAllRequestsTo|RedirectAllRequest|可选|**参数解释：**所有请求重定向规则，详见RedirectAllRequest。**约束限制：**key、suffix和routeRules必须配套使用，且与redirectAllRequestsTo互斥。当设置了这三个字段时，不能设置redirectAllRequestsTo；反之，当设置了redirectAllRequestsTo时，不能设置key、suffix和routeRules。设置redirectAllRequestsTo时不能为空。**默认取值：**无|


**表 4**  RedirectAllRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|hostName|String|必选|**参数解释：**重定向时使用的域名。如 www.example.com。**约束限制：**域名需符合域名规范。**默认取值：**无|
|protocol|ProtocolEnum|可选|**参数解释：**重定向时使用的协议。**取值范围：**详见ProtocolEnum。**默认取值：**无|


**表 5**  ProtocolEnum

|**常量名**|**原始值**|**说明**|
|--|--|--|
|HTTP|http|重定向请求时使用HTTP协议。|
|HTTPS|https|重定向请求时使用HTTPS协议。|


**表 6**  RouteRule

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|condition|RouteRuleCondition|可选|**参数解释：**重定向规则的匹配条件。详见RouteRuleCondition。|
|redirect|Redirect|必选|**参数解释：**重定向请求时的具体信息。详见Redirect。|


**表 7**  RouteRuleCondition

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|keyPrefixEquals|String|可选|**参数解释：**重定向生效时的对象名前缀。当向对象发送请求时，如果对象名前缀等于这个值，那么重定向生效。例如：重定向ExamplePage.html对象的请求，keyPrefixEquals设为ExamplePage.html。**约束限制：**与httpErrorCodeReturnedEquals参数不可同时使用，两者二选一。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|httpErrorCodeReturnedEquals|String|可选|**参数解释：**重定向生效时的HTTP错误码。当发生错误时，如果错误码等于这个值，那么重定向生效。例如：当返回的HTTP错误码为404时重定向到NotFound.html，可以将RouteRuleCondition中的httpErrorCodeReturnedEquals设置为404，Redirect中的replaceKeyWith设置为NotFound.html。**约束限制：**与keyPrefixEquals参数不可同时使用，两者二选一。**取值范围：**取值范围可参见错误码。**默认取值：**无|


**表 8**  Redirect

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|Protocol|ProtocolEnum|可选|**参数解释：**重定向时使用的协议。**取值范围：**详见ProtocolEnum。**默认取值：**无|
|hostName|String|可选|**参数解释：**重定向请求时使用的域名。**默认取值：**无|
|replaceKeyPrefixWith|String|可选|**参数解释：**重定向请求时使用的对象名前缀。**约束限制：**不可与replaceKeyWith同时使用。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|replaceKeyWith|String|可选|**参数解释：**重定向请求时使用的对象名。**约束限制：**不可与replaceKeyPrefixWith同时使用。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|httpRedirectCode|String|可选|**参数解释：**重定向请求时响应中的HTTP状态码，详见状态码。**默认取值：**无|


## 返回结果说明<a name="section1155011051819"></a>

**表 9**  返回结果HeaderResponse\(SDK公共响应结果\)各项属性说明

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|statusCode|int|**参数解释：**HTTP状态码。**取值范围：**状态码是一组从2xx（成功）到4xx或5xx（错误）的数字代码，状态码表示了请求响应的状态。完整的状态码列表请参见状态码。**默认取值：**无|
|responseHeaders|Map<String, Object>|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中String代表响应消息头的名称，Object代表响应消息头的值。**默认取值：**无|


## 代码示例：配置默认主页和错误页面<a name="section588794417493"></a>

以下代码展示了如何为examplebucket桶配置默认主页和错误页面。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.WebsiteConfiguration;
public class SetBucketWebsite001
{
    public static void main(String[] args) {
        // 您可以通过环境变量获取访问密钥AK/SK，也可以使用其他外部引入方式传入。如果使用硬编码可能会存在泄露风险。
        // 您可以登录访问管理控制台获取访问密钥AK/SK
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        String securityToken = System.getenv("SECURITY_TOKEN");
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
            // 以下代码展示了如何配置默认主页和错误页面
            WebsiteConfiguration config = new WebsiteConfiguration();
            // 配置默认主页
            config.setSuffix("index.html");
            // 配置错误页面
            config.setKey("error.html");
            obsClient.setBucketWebsite("examplebucket", config);
            System.out.println("setBucketWebsite successfully");
        } catch (ObsException e) {
            System.out.println("setBucketWebsite failed");
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
            System.out.println("setBucketWebsite failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：配置重定向规则<a name="section5890244114917"></a>

以下代码展示了如何为examplebucket桶配置重定向规则。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ProtocolEnum;
import com.obs.services.model.Redirect;
import com.obs.services.model.RouteRule;
import com.obs.services.model.RouteRuleCondition;
import com.obs.services.model.WebsiteConfiguration;
public class SetBucketWebsite002
{
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
            // 以下代码展示了如何配置重定向规则
            WebsiteConfiguration config = new WebsiteConfiguration();
            // 配置默认主页
            config.setSuffix("index.html");
            // 配置错误页面
            config.setKey("error.html");
            RouteRule rule = new RouteRule();
            Redirect r = new Redirect();
            r.setHostName("www.example.com");
            r.setHttpRedirectCode("305");
            r.setRedirectProtocol(ProtocolEnum.HTTP);
            r.setReplaceKeyPrefixWith("replacekeyprefix");
            rule.setRedirect(r);
            RouteRuleCondition condition = new RouteRuleCondition();
            condition.setHttpErrorCodeReturnedEquals("404");
            condition.setKeyPrefixEquals("keyprefix");
            rule.setCondition(condition);
            config.getRouteRules().add(rule);
            obsClient.setBucketWebsite("examplebucket", config);
            System.out.println("setBucketWebsite successfully");
        } catch (ObsException e) {
            System.out.println("setBucketWebsite failed");
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
            System.out.println("setBucketWebsite failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：配置所有请求重定向<a name="section13888144414494"></a>

以下代码展示了如何为examplebucket桶配置所有请求重定向。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.ProtocolEnum;
import com.obs.services.model.RedirectAllRequest;
import com.obs.services.model.WebsiteConfiguration;
public class SetBucketWebsite003
{
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
            // 以下代码展示了如何配置所有请求重定向
            WebsiteConfiguration config = new WebsiteConfiguration();
            RedirectAllRequest redirectAll = new RedirectAllRequest();
            redirectAll.setHostName("www.example.com");
            redirectAll.setRedirectProtocol(ProtocolEnum.HTTP);
            config.setRedirectAllRequestsTo(redirectAll);
            obsClient.setBucketWebsite("examplebucket", config);
            System.out.println("setBucketWebsite successfully");
        } catch (ObsException e) {
            System.out.println("setBucketWebsite failed");
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
            System.out.println("setBucketWebsite failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section143419113184"></a>

-   关于设置桶的托管配置的API说明，请参见[设置桶的网站配置](https://support.huaweicloud.com/api-obs/obs_04_0071.html)。
-   更多关于设置桶的托管配置的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/BucketOperationsSample.java)。
-   设置桶的托管配置过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   静态网站托管相关常见问题请参见[静态网站托管相关常见问题](https://support.huaweicloud.com/obs_faq/obs_faq_0500.html)。

