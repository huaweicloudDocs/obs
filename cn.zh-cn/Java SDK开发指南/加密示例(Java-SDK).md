# 加密示例\(Java SDK\)<a name="obs_21_1903"></a>

>![](public_sys-resources/icon-notice.gif) **须知：** 
>开发过程中，您有任何问题可以在github上[提交issue](https://github.com/huaweicloud/huaweicloud-sdk-java-obs/issues)，或者在[华为云对象存储服务论坛](https://bbs.huaweicloud.com/forum/forum-620-1.html)中发帖求助。

## 代码示例：上传对象加密（SSE-C方式）<a name="section14263193123819"></a>

以下代码展示了在上传对象时使用SSE-C方式进行服务端加密。

设置SSE-C方式下使用的密钥，请参考[如何生成SSE-C方式的加密密钥](https://support.huaweicloud.com/sdk-java-devg-obs/obs_21_2119.html)。

更多关于服务端加密的内容请参考[服务端加密SSE-C方式](https://support.huaweicloud.com/api-obs/obs_04_0107.html)。

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
// 认证用的ak和sk硬编码到代码中或者明文存储都有很大的安全风险，建议在配置文件或者环境变量中密文存放，使用时解密，确保安全；本示例以ak和sk保存在环境变量中为例，运行本示例前请先在本地环境中设置环境变量ACCESS_KEY_ID和SECRET_ACCESS_KEY_ID。
// 您可以登录访问管理控制台获取访问密钥AK/SK，获取方式请参见https://support.huaweicloud.com/usermanual-ca/ca_01_0003.html
String ak = System.getenv("ACCESS_KEY_ID");
String sk = System.getenv("SECRET_ACCESS_KEY_ID");
// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);

PutObjectRequest request = new PutObjectRequest();
request.setBucketName("bucketname");
request.setObjectKey("objectname");
request.setFile(new File("localfile"));

HashMap<String, String> userHeaders = new HashMap<>();
userHeaders.put("x-obs-server-side-encryption-customer-algorithm","AES256");
//SSE-C方式下使用该头域，该头域表示加密对象使用的密钥，头域值是256位密钥的base64编码。
userHeaders.put("x-obs-server-side-encryption-customer-key","your-encryption-customer-key");
userHeaders.put("x-obs-server-side-encryption-customer-key-MD5",
                    ServiceUtils.toBase64(ServiceUtils.computeMD5Hash(ServiceUtils.fromBase64("your-encryption-customer-key"))));            request.setUserHeaders(userHeaders);
HeaderResponse response = obsClient.putObject(request);
System.out.println("response:"+response.getRequestId());
```

## 代码示例：上传对象加密（SSE-OBS方式）<a name="section157019501914"></a>

以下代码展示了在上传对象时使用SSE-OBS方式进行服务端加密,通过自定义头域添加头域x-obs-server-side-encryption:AES256实现。

关于服务端加密的用户指南：[服务端加密](https://support.huaweicloud.com/ugobs-obs/obs_41_0035.html)。

```
// Endpoint以北京四为例，其他地区请按实际情况填写。
String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
// 认证用的ak和sk硬编码到代码中或者明文存储都有很大的安全风险，建议在配置文件或者环境变量中密文存放，使用时解密，确保安全；本示例以ak和sk保存在环境变量中为例，运行本示例前请先在本地环境中设置环境变量ACCESS_KEY_ID和SECRET_ACCESS_KEY_ID。
// 您可以登录访问管理控制台获取访问密钥AK/SK，获取方式请参见https://support.huaweicloud.com/usermanual-ca/ca_01_0003.html
String ak = System.getenv("ACCESS_KEY_ID");
String sk = System.getenv("SECRET_ACCESS_KEY_ID");
// 创建ObsClient实例
ObsClient obsClient = new ObsClient(ak, sk, endPoint);
//设置桶名、对象名、本地文件路径
PutObjectRequest request = new PutObjectRequest();
request.setBucketName("BucketName");
request.setObjectKey("ObjectKey");
request.setFile(new File("LocalFilePath"));
//设置自定义头域，设置使用sse-obs加密
HashMap<String, String> userHeaders = new HashMap<>();
userHeaders.put("x-obs-server-side-encryption","AES256");
request.setUserHeaders(userHeaders);
HeaderResponse response = obsClient.putObject(request);
```

## 代码示例：下载对象解密<a name="section0652153633818"></a>

以下代码展示了在下载对象时使用SSE-C方式进行服务端解密：

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.internal.utils.ServiceUtils;
import com.obs.services.model.GetObjectRequest;
import com.obs.services.model.ObsObject;
import java.util.HashMap;
import java.util.Map;

public class SseCGetObject{
    public static void main(String[] args) {
        // 认证用的ak和sk硬编码到代码中或者明文存储都有很大的安全风险，建议在配置文件或者环境变量中密文存放，使用时解密，确保安全；本示例以ak和sk保存在环境变量中为例，
        //运行本示例前请先在本地环境中设置环境变量ACCESS_KEY_ID和SECRET_ACCESS_KEY_ID。
        // 您可以登录访问管理控制台获取访问密钥AK/SK，获取方式请参见https://support.huaweicloud.com/usermanual-ca/ca_01_0003.html
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        // String securityToken = System.getenv("SECURITY_TOKEN");        
        // Endpoint以北京四为例，其他地区请按实际情况填写。
        String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";
        // 创建ObsClient实例,使用永久AK/SK初始化客户端
        ObsClient obsClient = new ObsClient(ak, sk,endPoint);
        // 使用临时AK/SK和SecurityToken初始化客户端
        // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

        try {
            // 调用接口进行操作，例如下载加密对象
            GetObjectRequest request=new GetObjectRequest("bucketname","objectname");
            // 设置SSE-C算法解密对象
            HashMap<String, String> userHeaders=new HashMap<>();
            userHeaders.put("x-obs-server-side-encryption-customer-algorithm","AES256");
            //SSE-C方式下使用该头域，该头域表示加密对象使用的密钥，头域值是256位密钥的base64编码。
            userHeaders.put("x-obs-server-side-encryption-customer-key","your-encryption-customer-key");
            userHeaders.put("x-obs-server-side-encryption-customer-key-MD5",
                    ServiceUtils.toBase64(ServiceUtils.computeMD5Hash(ServiceUtils.fromBase64("your-encryption-customer-key"))));
            request.setUserHeaders(userHeaders);
            ObsObject obsObject=obsClient.getObject(request);
            //可替换读取流的方法
            System.out.println(obsObject.getObjectContent());
        }
        catch(ObsException e) {
            System.out.println("putObject failed");
            // 请求失败,打印http状态码
            System.out.println("HTTP Code:" + e.getResponseCode());
            // 请求失败,打印服务端错误码
            System.out.println("Error Code:" + e.getErrorCode());
            // 请求失败,打印详细错误信息
            System.out.println("Error Message:" + e.getErrorMessage());
            // 请求失败,打印请求id
            System.out.println("Request ID:" + e.getErrorRequestId());
            System.out.println("Host ID:" + e.getErrorHostId());
            Map<String, String> headers=e.getResponseHeaders();
            if(headers!=null){
                // 遍历Map的entry打印所有报错相关头域
                for(Map.Entry<String, String> header:headers.entrySet()){
                    if(header.getKey().contains("error")){
                        System.out.println(header.getKey()+":"+header.getValue());
                    }
                }
            }
            e.printStackTrace();
        } catch (Exception e) {
            System.out.println("putObject failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

上传时使用SSE-OBS方式进行服务端加密的对象，下载、获取对象元数据时会自动解密，不用再附加加密相关头域，下载对象见[流式下载](流式下载(Java-SDK).md)，获取对象元数据见[获取对象元数据](获取对象元数据(Java-SDK).md)。

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   加密密钥的计算方式，可以参考章节：[如何生成SSE-C方式的加密密钥](如何生成SSE-C方式的加密密钥(Java-SDK).md)。

