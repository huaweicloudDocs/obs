# 临时授权方式实现图片处理\(Java SDK\)<a name="obs_21_0711"></a>

## 功能说明<a name="section1426243934613"></a>

OBS为用户提供了稳定、安全、高效、易用、低成本的图片处理服务。您可以通过临时授权方式传入图片处理参数，对图片文件进行图片剪切、图片缩放、图片水印、格式转换等处理。

更多关于图片处理的内容，参见[图片处理特性指南](http://support.huaweicloud.com/fg-obs/obs_01_0001.html)。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section19267102834710"></a>

-   您必须是桶拥有者或拥有下载对象的权限，才能下载对象。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:GetObject权限，如果使用桶策略则需授予GetObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。
-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

-   所有的图片处理操作均不会修改存储在桶中的原图。
-   归档存储不支持图片处理。
-   深度归档存储不支持图片处理。
-   处理后的图片直接返回浏览器展示，不会保存在OBS中，也不会占用存储空间，不会产生存储费用。图片处理只收取处理的费用。

## 方法定义<a name="section54232412"></a>

obsClient.createTemporarySignature\([TemporarySignatureRequest](#table91617616238) [request](#table14591111716211)\)

## 请求参数说明<a name="section29858833"></a>

**表 1**  createTemporarySignature请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|TemporarySignatureRequest|必选|**参数解释：**临时url创建请求参数列表，详见TemporarySignatureRequest。|


**表 2**  TemporarySignatureRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|可选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|可选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|specialParam|SpecialParamEnum|可选|**参数解释：**请求中可能用到的特殊参数，详见SpecialParamEnum。|
|method|HttpMethodEnum|必选|**参数解释：**HTTP方法类型，详见HttpMethodEnum。|
|headers|Map<String, String>|可选|**参数解释：**HTTP响应消息头列表，由多个元组构成。元组中第一个String代表响应消息头的名称，第二个String代表响应消息头的值。**默认取值：**无|
|queryParams|Map<String, Object>|可选|**参数解释：**请求中携带的查询参数。Map中类型为String的key代表request中的查询参数，类型为Obeject的value是查询参数取得的值。**默认取值：**无|
|expires|long|必选|**参数解释：**表示对象的过期时间（从对象最后修改时间开始计算），单位是天。过期之后对象会被自动删除。**约束限制：**此字段对于每个对象仅支持上传时配置，不支持后期通过修改元数据接口修改。**取值范围：**大于0的整型数，单位：天。**默认取值：**无|
|requestDate|Date|必选|**参数解释：**发起请求的时间。**默认取值：**无|


**表 3**  HttpMethodEnum & SpecialParamEnum

|**操作名**|**HTTP请求方法（OBS Java SDK对应值）**|**特殊操作符（OBS Java SDK对应值）**|**是否需要桶名**|**是否需要对象名**|
|--|--|--|--|--|
|创建桶|HttpMethodEnum.PUT|N/A|是|否|
|获取桶列表|HttpMethodEnum.GET|N/A|否|否|
|删除桶|HttpMethodEnum.DELETE|N/A|是|否|
|列举桶内对象|HttpMethodEnum.GET|N/A|是|否|
|列举桶内多版本对象|HttpMethodEnum.GET|SpecialParamEnum.VERSIONS|是|否|
|列举分段上传任务|HttpMethodEnum.GET|SpecialParamEnum.UPLOADS|是|否|
|获取桶元数据|HttpMethodEnum.HEAD|N/A|是|否|
|获取桶区域位置|HttpMethodEnum.GET|SpecialParamEnum.LOCATION|是|否|
|获取桶存量信息|HttpMethodEnum.GET|SpecialParamEnum.STORAGEINFO|是|否|
|设置桶配额|HttpMethodEnum.PUT|SpecialParamEnum.QUOTA|是|否|
|获取桶配额|HttpMethodEnum.GET|SpecialParamEnum.QUOTA|是|否|
|设置桶存储类别|HttpMethodEnum.PUT|SpecialParamEnum.STORAGEPOLICY|是|否|
|获取桶存储类别|HttpMethodEnum.GET|SpecialParamEnum.STORAGEPOLICY|是|否|
|设置桶访问权限|HttpMethodEnum.PUT|SpecialParamEnum.ACL|是|否|
|获取桶访问权限|HttpMethodEnum.GET|SpecialParamEnum.ACL|是|否|
|开启/关闭桶日志|HttpMethodEnum.PUT|SpecialParamEnum.LOGGING|是|否|
|查看桶日志|HttpMethodEnum.GET|SpecialParamEnum.LOGGING|是|否|
|设置桶策略|HttpMethodEnum.PUT|SpecialParamEnum.POLICY|是|否|
|查看桶策略|HttpMethodEnum.GET|SpecialParamEnum.POLICY|是|否|
|删除桶策略|HttpMethodEnum.DELETE|SpecialParamEnum.POLICY|是|否|
|设置生命周期规则|HttpMethodEnum.PUT|SpecialParamEnum.LIFECYCLE|是|否|
|查看生命周期规则|HttpMethodEnum.GET|SpecialParamEnum.LIFECYCLE|是|否|
|删除生命周期规则|HttpMethodEnum.DELETE|SpecialParamEnum.LIFECYCLE|是|否|
|设置托管配置|HttpMethodEnum.PUT|SpecialParamEnum.WEBSITE|是|否|
|查看托管配置|HttpMethodEnum.GET|SpecialParamEnum.WEBSITE|是|否|
|清除托管配置|HttpMethodEnum.DELETE|SpecialParamEnum.WEBSITE|是|否|
|设置桶多版本状态|HttpMethodEnum.PUT|SpecialParamEnum.VERSIONING|是|否|
|查看桶多版本状态|HttpMethodEnum.GET|SpecialParamEnum.VERSIONING|是|否|
|设置跨域规则|HttpMethodEnum.PUT|SpecialParamEnum.CORS|是|否|
|查看跨域规则|HttpMethodEnum.GET|SpecialParamEnum.CORS|是|否|
|删除跨域规则|HttpMethodEnum.DELETE|SpecialParamEnum.CORS|是|否|
|设置桶标签|HttpMethodEnum.PUT|SpecialParamEnum.TAGGING|是|否|
|查看桶标签|HttpMethodEnum.GET|SpecialParamEnum.TAGGING|是|否|
|删除桶标签|HttpMethodEnum.DELETE|SpecialParamEnum.TAGGING|是|否|
|上传对象|HttpMethodEnum.PUT|N/A|是|是|
|追加上传|HttpMethodEnum.POST|SpecialParamEnum.APPEND|是|是|
|下载对象|HttpMethodEnum.GET|N/A|是|是|
|复制对象|HttpMethodEnum.PUT|N/A|是|是|
|删除对象|HttpMethodEnum.DELETE|N/A|是|是|
|批量删除对象|HttpMethodEnum.POST|SpecialParamEnum.DELETE|是|是|
|获取对象属性|HttpMethodEnum.HEAD|N/A|是|是|
|设置对象访问权限|HttpMethodEnum.PUT|SpecialParamEnum.ACL|是|是|
|查看对象访问权限|HttpMethodEnum.GET|SpecialParamEnum.ACL|是|是|
|初始化分段上传任务|HttpMethodEnum.POST|SpecialParamEnum.UPLOADS|是|是|
|上传段|HttpMethodEnum.PUT|N/A|是|是|
|复制段|HttpMethodEnum.PUT|N/A|是|是|
|列举已上传的段|HttpMethodEnum.GET|N/A|是|是|
|合并段|HttpMethodEnum.POST|N/A|是|是|
|取消分段上传任务|HttpMethodEnum.DELETE|N/A|是|是|
|恢复归档存储对象|HttpMethodEnum.POST|SpecialParamEnum.RESTORE|是|是|


## 返回结果说明<a name="section1155011051819"></a>

**表 4**  TemporarySignatureResponse

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|signedUrl|String|**参数解释：**带授权信息的URL。**默认取值：**无|
|actualSignedRequestHeaders|Map<String, String>|**参数解释：**通过带授权信息的URL发起请求时实际应携带的头域。**默认取值：**无|


## 代码示例<a name="section7239145884616"></a>

以下代码展示了通过临时授权方式实现图片处理，对examplebucket桶里的objectname.jpg对象进行缩放，旋转。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import java.util.HashMap;
import java.util.Map;
public class GetObject009 {
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
            // 通过临时授权方式实现图片处理
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname.jpg");
            // 设置图片处理参数，对图片依次进行缩放、旋转
            Map<String, Object> queryParams = new HashMap<String, Object>();
            queryParams.put("x-image-process", "image/resize,m_fixed,w_100,h_100/rotate,90");
            request.setQueryParams(queryParams);
            // 生成临时授权URL
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("getSignedUrl successfully");
            System.out.println(response.getSignedUrl());
        } catch (ObsException e) {
            System.out.println("getSignedUrl failed");
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
            System.out.println("getSignedUrl failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 相关链接<a name="section520381913719"></a>

-   关于图片处理的更多信息，请参见[图片处理](https://support.huaweicloud.com/fg-obs/obs_01_0001.html)。
-   图片处理过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   图片处理常见问题请参见[图片处理常见问题](https://support.huaweicloud.com/fg-obs/obs_01_0600.html)。

