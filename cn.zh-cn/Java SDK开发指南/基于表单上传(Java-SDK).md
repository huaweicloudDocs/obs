# 基于表单上传\(Java SDK\)<a name="obs_21_0612"></a>

## 功能说明<a name="section15605512"></a>

基于表单上传是使用HTML表单形式上传对象到指定桶中，对象最大不能超过5GB。

您可以通过ObsClient.createPostSignature生成基于表单上传的请求参数。使用代码模拟表单上传的完整代码示例，参见[PostObjectSample](https://obssdk.obs.cn-north-1.myhuaweicloud.com/sample/java/PostObjectSample.zip)。您也可以通过如下步骤进行表单上传： 

1.  使用ObsClient.createPostSignature生成用于鉴权的请求参数。
2.  准备表单HTML页面。
3.  将生成的请求参数填入HTML页面。
4.  选择本地文件，进行表单上传。

>![](public_sys-resources/icon-note.gif) **说明：** 
>使用SDK生成的用于鉴权的请求参数包括两个：
>-   Policy，对应表单中policy字段。
>-   Signature，对应表单中的signature字段。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 接口约束<a name="section1657513244315"></a>

-   您必须是桶拥有者或拥有上传对象的权限，才能上传对象。建议使用IAM或桶策略进行授权，如果使用IAM则需授予obs:object:PutObject权限，如果使用桶策略则需授予PutObject权限。相关授权方式介绍可参见[OBS权限控制概述](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0001.html)，配置方式详见[使用IAM自定义策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0121.html)、[配置对象策略](https://support.huaweicloud.com/usermanual-obs/obs_03_0075.html)。

-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。
-   HTML表单中的policy，signature的值均是从ObsClient.createPostSignature的返回结果中获取。
-   上传对象 contentType字段需要手动修改为对应的Content-Type值。
-   在设置对象ACL权限时，HTML表单中的acl取值参见  [OBS预定义的权限控制策略](https://support.huaweicloud.com/perms-cfg-obs/obs_40_0005.html#section3)。
-   您可以直接下载表单HTML示例[PostDemo](https://obssdk.obs.cn-north-1.myhuaweicloud.com/sample/java/PostDemo.zip)。

## 方法定义<a name="section54232412"></a>

obsClient.createPostSignature\([PostSignatureRequest](#table9147151314100) [request](#table1824117496403)\)

**表 1**  createPostSignature请求参数

|**参数**|**类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|PostSignatureRequest|是|**参数解释：**基于表单上传请求参数，详见PostSignatureRequest。|


**表 2**  PostSignatureRequest

|**参数**|**类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|可选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|可选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|requestDate|Date|可选|**参数解释：**发起请求的时间。**默认取值：**无|
|expiryDate|Date|可选|**参数解释：**有效截止日期。**默认取值：**无|
|expires|long|可选|**参数解释：**表单上传鉴权的过期时间。**取值范围：**大于0的整型数。单位：秒。**默认取值：**300|
|conditions|List<String>|可选|**参数解释**：设置表单限制条件，如果设置了该值，将直接使用该值计算policy而忽略请求的表单参数中的设置。**默认取值：**无|
|formParams|Map<String, Object>|可选|**参数解释**：请求的表单参数。参数列表Map中String为请求时的表单参数名称，Object为对应表单参数名称的取值。**默认取值：**无|


## 返回结果说明<a name="section350311507317"></a>

**表 3**  PostSignatureResponse

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|OriginPolicy|String|**参数解释：**Policy未经过Base64之前的值，仅用于校验。示例如下：{"expiration":"2023-09-12T12:52:59Z","conditions":[{"content-type":"text/plain"},{"bucket":"examplebucket"},{"key":"example/objectname"},]}"**默认取值：**无|
|Policy|String|**参数解释：**表单中的policy，已经Base64之后的值。示例如下：eyJleHBpcmF0aW9uIjoiMjAyMy0wOS0xMlQxMjo1Mjo1OVoiLCJjb25kaXRpb25zIjpbeyJjb250ZW50LXR5cGUiOiJ0ZXh0L3BsYWluIn0seyJidWNrZXQiOiJleGFtcGxlYnVja2V0In0seyJrZXkiOiJleGFtcGxlL29iamVjdG5hbWUifSxdfQ==**默认取值：**无|
|Signature|String|**参数解释：**表单中的signature。示例如下：g0jQr4v9VWd1Q2FOFDG6LGfV9Cw=**默认取值：**无|


## 代码示例<a name="section6502203112390"></a>

此用例用于生成带授权信息的表单上传参数policy和signature。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.PostSignatureRequest;
import com.obs.services.model.PostSignatureResponse;
import java.util.HashMap;
import java.util.Map;
public class PostObject001 {
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
            // 生成基于表单上传的请求
            PostSignatureRequest request = new PostSignatureRequest();
            // 设置表单参数
            Map<String, Object> formParams = new HashMap<String, Object>();
            // 设置对象访问权限为公共读
            formParams.put("x-obs-acl", "public-read");
            // 设置对象MIME类型
            formParams.put("content-type", "text/plain");
            request.setFormParams(formParams);
            // 设置表单上传请求有效期，单位：秒
            request.setExpires(3600);
            PostSignatureResponse response = obsClient.createPostSignature(request);
            System.out.println("createPostSignature successfully");
            // 获取表单上传请求参数
            System.out.println("Policy:" + response.getPolicy());
            System.out.println("Signature:" + response.getSignature());
        } catch (ObsException e) {
            System.out.println("createPostSignature failed");
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
            System.out.println("createPostSignature failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}

```

示例表单HTML代码如下：

```
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
<form action="http://bucketname.your-endpoint/" method="post" enctype="multipart/form-data">
    Object key
    <!-- 对象名 -->
    <input type="text" name="key" value="objectname" />
    <p>
        ACL
        <!-- 对象ACL权限 -->
        <input type="text" name="x-obs-acl" value="public-read" />
    <p>
        Content-Type
        <!-- 对象MIME类型 -->
        <input type="text" name="content-type" value="text/plain" />
    <p>
        <!-- 直接使用PostSignatureResponse.getPolicy()返回的值 -->
        <input type="hidden" name="policy" value="*** Provide your policy ***" />
        <!-- AK -->
        <input type="hidden" name="AccessKeyId" value="*** Provide your access key ***"/>
        <!-- 签名串信息 -->
        <input type="hidden" name="signature" value="*** Provide your signature ***"/>
        <input name="file" type="file" />
        <input name="submit" value="Upload" type="submit" />
</form>
</body>
</html>
```

## 相关链接<a name="section520381913719"></a>

-   关于上传对象-POST上传的API说明，请参见[POST上传](https://support.huaweicloud.com/api-obs/obs_04_0081.html)。
-   更多关于上传对象的示例代码，请参见[Github示例](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/blob/master/app/src/test/java/samples_java/PostObjectSample.java)。
-   上传对象过程中返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。
-   上传对象常见问题请参见[上传对象失败](https://support.huaweicloud.com/obs_faq/obs_faq_0134.html)。

