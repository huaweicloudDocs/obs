# 通过临时URL访问OBS\(Java SDK\)<a name="obs_21_0901"></a>

## 功能说明<a name="section129642317504"></a>

OBS客户端支持通过访问密钥、请求方法类型、请求参数等信息生成一个在Query参数中携带鉴权信息的URL，可将该URL提供给其他用户进行临时访问。在生成URL时，您需要指定URL的有效期来限制访客用户的访问时长。

如果您想授予其他用户对桶或对象临时进行其他操作的权限（例如上传或下载对象），则需要生成带对应请求的URL后（例如使用生成PUT请求的URL上传对象），将该URL提供给其他用户。

如果遇到跨域报错、签名不匹配问题，请参考以下步骤排查问题：

1.  未配置跨域，需要在控制台配置CORS规则，请参考[配置桶允许跨域请求](https://support.huaweicloud.com/sdk-browserjs-devg-obs/obs_24_0107.html)。
2.  签名计算问题，请参考[URL中携带签名](https://support.huaweicloud.com/api-obs/obs_04_0011.html)排查签名参数是否正确；比如上传对象功能，后端将Content-Type参与计算签名生成授权URL，但是前端使用授权URL时没有设置Content-Type字段或者传入错误的值，此时会出现跨域错误。解决方案为：Content-Type字段前后端保持一致。
3.  不支持通过CDN加速后的域名生成临时访问URL。

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

通过该方式可支持的操作以及相关信息见下表：

**表 1**  HttpMethodEnum & SpecialParamEnum

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


通过OBS Java SDK生成临时URL访问OBS的步骤如下：

1.  通过ObsClient.createTemporarySignature生成带签名信息的URL。
2.  使用任意HTTP库发送HTTP/HTTPS请求，访问OBS服务。

## 接口约束<a name="section17324757115011"></a>

-   OBS支持的region以及region与endPoint的对应关系，详细信息请参见[地区与终端节点](https://developer.huaweicloud.com/endpoint?OBS)。

## 方法定义<a name="section1047625816448"></a>

obsClient.createTemporarySignature\([TemporarySignatureRequest](#table91617616238) [request](#table14591111716211)\)

## 请求参数说明<a name="section239664412131"></a>

**表 2**  请求参数列表

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|request|TemporarySignatureRequest|必选|**参数解释：**临时url创建请求，详见TemporarySignatureRequest。|


**表 3**  TemporarySignatureRequest

|**参数名称**|**参数类型**|**是否必选**|**描述**|
|--|--|--|--|
|bucketName|String|可选|**参数解释：**桶名。**约束限制：**桶的名字需全局唯一，不能与已有的任何桶名称重复，包括其他用户创建的桶。桶命名规则如下：3～63个字符，数字或字母开头，支持小写字母、数字、“-”、“.”。禁止使用IP地址。禁止以“-”或“.”开头及结尾。禁止两个“.”相邻（如：“my..bucket”）。禁止“.”和“-”相邻（如：“my-.bucket”和“my.-bucket”）。同一用户在同一个区域多次创建同名桶不会报错，创建的桶属性以第一次请求为准。**默认取值：**无|
|objectKey|String|可选|**参数解释：**对象名。对象名是对象在存储桶中的唯一标识。对象名是对象在桶中的完整路径，路径中不包含桶名。例如，您对象的访问地址为examplebucket.obs.cn-north-4.myhuaweicloud.com/folder/test.txt 中，对象名为folder/test.txt。**取值范围：**长度大于0且不超过1024的字符串。**默认取值：**无|
|specialParam|SpecialParamEnum|可选|**参数解释：**请求中可能用到的特殊参数，代表要操作的子资源。**取值范围：**详见SpecialParamEnum。**默认取值：**无|
|method|HttpMethodEnum|必选|**参数解释：**HTTP方法类型。**取值范围：**详见HttpMethodEnum。**默认取值：**无|
|headers|Map<String, String>|可选|**参数解释：**请求中携带的头域。请求头域列表Map中第一个String代表请求头域的名称，第二个String代表对应请求头域名称的取值。**默认取值：**无|
|queryParams|Map<String, Object>|可选|**参数解释：**请求中携带的查询参数。参数列表Map中的String为查询参数的名称，Object为对应查询参数名称的取值。**默认取值：**无|
|expires|long|必选|**参数解释：**带授权信息的URL的过期时间。**取值范围：**大于等于0的整型数，单位：秒。**默认取值：**300秒|
|requestDate|Date|必选|**参数解释：**发起请求的时间。**默认取值：**无|


## 返回结果说明<a name="section18477105884811"></a>

**表 4**  TemporarySignatureResponse

|**参数名称**|**参数类型**|**描述**|
|--|--|--|
|signedUrl|String|**参数解释：**带授权信息的URL。**默认取值：**无|
|actualSignedRequestHeaders|Map<String, String>|**参数解释：**通过带授权信息的URL发起请求时实际应携带的头域。头域列表Map中第一个String为请求头域的名称，第二个String为对应请求头域名称的取值。**默认取值：**无|


## 代码示例：创建桶<a name="section8517109534"></a>

临时授权访问，利用HttpMethodEnum.PUT请求创建examplebucket桶，URL有效期设置为3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import okhttp3.Call;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;
import java.util.Map;
public class CreateBucket001 {
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
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.PUT, expireSeconds);
            request.setBucketName("examplebucket");
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("Creating bucket using temporary signature url:");
            System.out.println("\t" + response.getSignedUrl());
            Request.Builder builder = new Request.Builder();
            for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                builder.header(entry.getKey(), entry.getValue());
            }
            // 使用PUT请求创建桶
            String location = "your bucket location";
            Request httpRequest =
                    builder.url(response.getSignedUrl())
                            .put(
                                    RequestBody.create(
                                            null,
                                            "<CreateBucketConfiguration><Location>"
                                                    + location
                                                    + "</Location></CreateBucketConfiguration>".getBytes()))
                            .build();
            OkHttpClient httpClient =
                    new OkHttpClient.Builder()
                            .followRedirects(false)
                            .retryOnConnectionFailure(false)
                            .cache(null)
                            .build();
            Call c = httpClient.newCall(httpRequest);
            Response res = c.execute();
            System.out.println("\tStatus:" + res.code());
            if (res.body() != null) {
                System.out.println("\tContent:" + res.body().string() + "\n");
            }
            res.close();
            System.out.println("CreateBucket successfully");
        } catch (ObsException e) {
            System.out.println("CreateBucket failed");
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
            System.out.println("CreateBucket failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：上传对象<a name="section1057571281111"></a>

临时授权访问，利用HttpMethodEnum.PUT请求上传对象到examplebucket桶下的objectname对象中，URL有效期设置为3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import okhttp3.Call;
import okhttp3.MediaType;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;
import java.util.HashMap;
import java.util.Map;
public class PutObject001 {
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
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            Map<String, String> headers = new HashMap<>();
            String contentType = "text/plain";
            headers.put("Content-Type", contentType);
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.PUT, expireSeconds);
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname");
            request.setHeaders(headers);
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("Creating object using temporary signature url:");
            System.out.println("\t" + response.getSignedUrl());
            Request.Builder builder = new Request.Builder();
            for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                builder.header(entry.getKey(), entry.getValue());
            }
            // 使用PUT请求上传对象
            Request httpRequest =
                    builder.url(response.getSignedUrl())
                            .put(RequestBody.create(MediaType.parse(contentType), "Hello OBS".getBytes("UTF-8")))
                            .build();
            OkHttpClient httpClient =
                    new OkHttpClient.Builder()
                            .followRedirects(false)
                            .retryOnConnectionFailure(false)
                            .cache(null)
                            .build();
            Call c = httpClient.newCall(httpRequest);
            Response res = c.execute();
            System.out.println("Status:" + res.code());
            if (res.body() != null) {
                System.out.println("Content:" + res.body().string() + "\n");
            }
            res.close();
            System.out.println("PutObject successfully");
        } catch (ObsException e) {
            System.out.println("PutObject failed");
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
            System.out.println("PutObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：下载对象<a name="section1382216339118"></a>

临时授权访问，利用HttpMethodEnum.GET请求下载examplebucket桶下的objectname对象，URL有效期设置为3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import okhttp3.Call;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import java.io.InputStream;
import java.util.Map;
public class GetObject001 {
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
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname");
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("Getting object using temporary signature url:");
            System.out.println("SignedUrl:" + response.getSignedUrl());
            Request.Builder builder = new Request.Builder();
            for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                builder.header(entry.getKey(), entry.getValue());
            }
            // 使用GET请求下载对象
            Request httpRequest = builder.url(response.getSignedUrl()).get().build();
            OkHttpClient httpClient =
                    new OkHttpClient.Builder()
                            .followRedirects(false)
                            .retryOnConnectionFailure(false)
                            .cache(null)
                            .build();
            Call c = httpClient.newCall(httpRequest);
            Response res = c.execute();
            System.out.println("Status:" + res.code());
            InputStream objectContent = null;
            if (res.body() != null) {
                objectContent = res.body().byteStream();
                System.out.println("Content:" + res.body().string() + "\n");
            }
            if(objectContent != null) {
                // objectContent 就是获取的要下载的文件的文件流
                // 在这里可以读取 objectContent，长时间不读取这个流会被服务端断开连接
            }
            res.close();
            System.out.println("getObject successfully");
        } catch (ObsException e) {
            System.out.println("getObject failed");
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
            System.out.println("getObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：列举对象<a name="section20628113717110"></a>

临时授权访问，利用HttpMethodEnum.GET请求列举examplebucket桶下的对象，URL有效期设置为3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import okhttp3.Call;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import java.util.Map;
public class ListObject001 {
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
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
            request.setBucketName("examplebucket");
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("Getting object list using temporary signature url:");
            System.out.println("\t" + response.getSignedUrl());
            Request.Builder builder = new Request.Builder();
            for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                builder.header(entry.getKey(), entry.getValue());
            }
            // 使用GET请求获取对象列表
            Request httpRequest = builder.url(response.getSignedUrl()).get().build();
            OkHttpClient httpClient =
                    new OkHttpClient.Builder()
                            .followRedirects(false)
                            .retryOnConnectionFailure(false)
                            .cache(null)
                            .build();
            Call c = httpClient.newCall(httpRequest);
            Response res = c.execute();
            System.out.println("Status:" + res.code());
            if (res.body() != null) {
                System.out.println("Content:" + res.body().string() + "\n");
            }
            res.close();
            System.out.println("ListObject successfully");
        } catch (ObsException e) {
            System.out.println("ListObject failed");
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
            System.out.println("ListObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：删除对象<a name="section0796203914111"></a>

临时授权访问，利用HttpMethodEnum.DELETE请求删除examplebucket桶下的objectname对象，URL有效期设置3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import okhttp3.Call;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import java.util.Map;
public class DeleteObject001 {
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
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.DELETE, expireSeconds);
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname");
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("Deleting object using temporary signature url:");
            System.out.println("\t" + response.getSignedUrl());
            Request.Builder builder = new Request.Builder();
            for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                builder.header(entry.getKey(), entry.getValue());
            }
            // 使用DELETE删除对象
            Request httpRequest = builder.url(response.getSignedUrl()).delete().build();
            OkHttpClient httpClient =
                    new OkHttpClient.Builder()
                            .followRedirects(false)
                            .retryOnConnectionFailure(false)
                            .cache(null)
                            .build();
            Call c = httpClient.newCall(httpRequest);
            Response res = c.execute();
            System.out.println("\tStatus:" + res.code());
            if (res.body() != null) {
                System.out.println("\tContent:" + res.body().string() + "\n");
            }
            res.close();
            System.out.println("deleteObjects successfully");
        } catch (ObsException e) {
            System.out.println("deleteObjects failed");
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
            System.out.println("deleteObjects failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：初始化分段上传任务<a name="section57571639329"></a>

临时授权访问，利用HttpMethodEnum.POST请求实现分段上传初始化，URL有效期设置3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.SpecialParamEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import okhttp3.Call;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;
import java.util.Map;
public class InitiateMultiPartUpload001 {
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
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.POST, expireSeconds);
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname");
            request.setSpecialParam(SpecialParamEnum.UPLOADS);
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("initiate multipart upload using temporary signature url:");
            System.out.println("\t" + response.getSignedUrl());
            Request.Builder builder = new Request.Builder();
            for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                builder.header(entry.getKey(), entry.getValue());
            }
            // 使用POST请求初始化分段上传任务
            Request httpRequest = builder.url(response.getSignedUrl()).post(RequestBody.create(null, "")).build();
            OkHttpClient httpClient =
                    new OkHttpClient.Builder()
                            .followRedirects(false)
                            .retryOnConnectionFailure(false)
                            .cache(null)
                            .build();
            Call c = httpClient.newCall(httpRequest);
            Response res = c.execute();
            System.out.println("Status:" + res.code());
            if (res.body() != null) {
                System.out.println("Content:" + res.body().string() + "\n");
            }
            res.close();
            System.out.println("InitiateMultiPartUpload successfully");
        } catch (ObsException e) {
            System.out.println("InitiateMultiPartUpload failed");
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
            System.out.println("InitiateMultiPartUpload failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：上传段<a name="section43006123611"></a>

临时授权访问，利用HttpMethodEnum.PUT请求实现上传段，URL有效期设置3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import okhttp3.Call;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;
import java.util.HashMap;
import java.util.Map;
public class UploadPart001 {
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
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.PUT, expireSeconds);
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname");
            Map<String, Object> queryParams = new HashMap<String, Object>();
            // 设置partNumber请求参数，例如：queryParams.put("partNumber", "1");
            queryParams.put("partNumber", "partNumber");
            queryParams.put("uploadId", "your uploadId");
            request.setQueryParams(queryParams);
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("upload part using temporary signature url:");
            System.out.println("SignedUrl:" + response.getSignedUrl());
            Request.Builder builder = new Request.Builder();
            for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                builder.header(entry.getKey(), entry.getValue());
            }
            // 使用PUT请求上传段
            Request httpRequest =
                    builder.url(response.getSignedUrl())
                            .put(RequestBody.create(null, new byte[6 * 1024 * 1024]))
                            .build();
            OkHttpClient httpClient =
                    new OkHttpClient.Builder()
                            .followRedirects(false)
                            .retryOnConnectionFailure(false)
                            .cache(null)
                            .build();
            Call c = httpClient.newCall(httpRequest);
            Response res = c.execute();
            System.out.println("Status:" + res.code());
            if (res.body() != null) {
                System.out.println("Content:" + res.body().string() + "\n");
            }
            res.close();
            System.out.println("UploadPart successfully");
        } catch (ObsException e) {
            System.out.println("UploadPart failed");
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
            System.out.println("UploadPart failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：列举已上传段<a name="section14449204412281"></a>

临时授权访问，利用HttpMethodEnum.GET请求实现列举已上传段，URL有效期设置3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import okhttp3.Call;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import java.util.HashMap;
import java.util.Map;
public class ListUploadedParts001 {
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
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname");
            Map<String, Object> queryParams = new HashMap<String, Object>();
            queryParams.put("uploadId", "your uploadId");
            request.setQueryParams(queryParams);
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("list parts using temporary signature url:");
            System.out.println("\t" + response.getSignedUrl());
            Request.Builder builder = new Request.Builder();
            for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                builder.header(entry.getKey(), entry.getValue());
            }
            // 使用GET请求列举已上传段
            Request httpRequest = builder.url(response.getSignedUrl()).get().build();
            OkHttpClient httpClient =
                    new OkHttpClient.Builder()
                            .followRedirects(false)
                            .retryOnConnectionFailure(false)
                            .cache(null)
                            .build();
            Call c = httpClient.newCall(httpRequest);
            Response res = c.execute();
            System.out.println("Status:" + res.code());
            if (res.body() != null) {
                System.out.println("Content:" + res.body().string() + "\n");
            }
            res.close();
            System.out.println("ListParts successfully");
        } catch (ObsException e) {
            System.out.println("ListParts failed");
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
            System.out.println("ListParts failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：合并段<a name="section27861832937"></a>

临时授权访问，利用HttpMethodEnum.POST请求实现合并段，URL有效期设置3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import okhttp3.Call;
import okhttp3.MediaType;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;
import java.util.HashMap;
import java.util.Map;
public class CompleteMultiPartUpload001 {
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
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.POST, expireSeconds);
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname");
            Map<String, String> headers = new HashMap<>();
            String contentType = "application/xml";
            headers.put("Content-Type", contentType);
            request.setHeaders(headers);
            Map<String, Object> queryParams = new HashMap<>();
            queryParams.put("uploadId", "your uploadId");
            request.setQueryParams(queryParams);
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("complete multipart upload using temporary signature url:");
            System.out.println("\t" + response.getSignedUrl());
            Request.Builder builder = new Request.Builder();
            for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                builder.header(entry.getKey(), entry.getValue());
            }
            // 以下content为示例代码，需要通过列举已上传段方法的响应结果，拼装以下内容
            String content = "<CompleteMultipartUpload>";
            content += "<Part>";
            content += "<PartNumber>1</PartNumber>";
            content += "<ETag>da6a0d097e307ac52ed9b4ad551801fc</ETag>";
            content += "</Part>";
            content += "<Part>";
            content += "<PartNumber>2</PartNumber>";
            content += "<ETag>da6a0d097e307ac52ed9b4ad551801fc</ETag>";
            content += "</Part>";
            content += "</CompleteMultipartUpload>";
            // 使用POST请求合并段
            Request httpRequest =
                    builder.url(response.getSignedUrl())
                            .post(RequestBody.create(MediaType.parse(contentType), content.getBytes("UTF-8")))
                            .build();
            OkHttpClient httpClient =
                    new OkHttpClient.Builder()
                            .followRedirects(false)
                            .retryOnConnectionFailure(false)
                            .cache(null)
                            .build();
            Call c = httpClient.newCall(httpRequest);
            Response res = c.execute();
            System.out.println("\tStatus:" + res.code());
            if (res.body() != null) {
                System.out.println("\tContent:" + res.body().string() + "\n");
            }
            res.close();
        } catch (ObsException e) {
            System.out.println("CompleteMultiPartUpload failed");
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
            System.out.println("CompleteMultiPartUpload failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：获取图片转码的下载链接<a name="section112801918071"></a>

临时授权访问，利用HttpMethodEnum.GET请求实现获取图片转码的下载链接，URL有效期设置3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import java.util.HashMap;
import java.util.Map;
public class GetObject002 {
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
            // 获取图片转码的下载链接
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname");
            // 设置图片转码参数
            Map<String, Object> queryParams = new HashMap<String, Object>();
            queryParams.put("x-image-process", "image/resize,m_fixed,w_100,h_100/rotate,100");
            request.setQueryParams(queryParams);
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            // 获取支持图片转码的下载链接
            System.out.println("Getting object using temporary signature url:");
            System.out.println("SignedUrl:" + response.getSignedUrl());
        } catch (ObsException e) {
            System.out.println("getObject failed");
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
            System.out.println("getObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

## 代码示例：下载SSE-C加密类型的对象<a name="section195111828105617"></a>

临时授权访问，利用HttpMethodEnum.GET请求实现下载SSE-C加密类型的对象，URL有效期设置3600秒。

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.HttpMethodEnum;
import com.obs.services.model.TemporarySignatureRequest;
import com.obs.services.model.TemporarySignatureResponse;
import okhttp3.Call;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import java.util.HashMap;
import java.util.Map;
public class GetObject003 {
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
            // 下载SSE-C加密类型的对象
            // URL有效期，3600秒
            long expireSeconds = 3600L;
            TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
            request.setBucketName("examplebucket");
            request.setObjectKey("objectname");
            // 设置SSE-C加密方式的头域信息
            Map<String, String> headers = new HashMap<>();
            headers.put("x-obs-server-side-encryption-customer-algorithm", "AES256");
            // 设置加密使用的密钥，该头域由256-bit的密钥经过base64-encoded得到
            headers.put(
                    "x-obs-server-side-encryption-customer-key",
                    "your base64 sse-c key generated by AES-256 algorithm");
            // 设置加密使用的密钥的MD5值，该头域由密钥的128-bit MD5值经过base64-encoded得到
            headers.put("x-obs-server-side-encryption-customer-key-MD5", "the md5 value of your sse-c key");
            request.setHeaders(headers);
            TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
            System.out.println("Getting object using temporary signature url:");
            System.out.println("\t" + response.getSignedUrl());
            Request.Builder builder = new Request.Builder();
            for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                builder.header(entry.getKey(), entry.getValue());
            }
            // 使用GET请求下载对象
            Request httpRequest = builder.url(response.getSignedUrl()).get().build();
            OkHttpClient httpClient =
                    new OkHttpClient.Builder()
                            .followRedirects(false)
                            .retryOnConnectionFailure(false)
                            .cache(null)
                            .build();
            Call c = httpClient.newCall(httpRequest);
            Response res = c.execute();
            System.out.println("Status:" + res.code());
            if (res.body() != null) {
                System.out.println("Content:" + res.body().string() + "\n");
            }
            res.close();
            System.out.println("getObject successfully");
        } catch (ObsException e) {
            System.out.println("getObject failed");
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
            System.out.println("getObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   HttpMethodEnum是OBS Java SDK定义的枚举类型，代表请求方法类型。
>-   加密密钥的计算方式，可以参考章节：[如何生成SSE-C方式的加密密钥](如何生成SSE-C方式的加密密钥(Java-SDK).md)。

## 相关链接<a name="section3780185512367"></a>

-   更多URL携带签名信息参考[url中携带签名](https://support.huaweicloud.com/api-obs/obs_04_0011.html)。
-   服务端加密接口返回的错误码含义、问题原因及处理措施可参考[OBS错误码](https://support.huaweicloud.com/api-obs/obs_04_0115.html#section1)。

