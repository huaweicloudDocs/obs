# 如何指定Content-SHA256?\(Java SDK\)<a name="obs_21_2122"></a>

上传对象和上传段支持携带x-obs-content-sha256头域，该头域值为请求消息体256-bit SHA256值转十六进制值，计算方式为Hex\(SHA256Hash\(<payload\>\)，服务端会对携带此头域的请求计算其消息体的sha256值做校验（性能会有部分下降，在安全上推荐该算法），上传对象示例代码如下：

```
import com.obs.services.ObsClient;
import com.obs.services.exception.ObsException;
import com.obs.services.model.PutObjectRequest;

import java.io.File;
import java.io.InputStream;
import java.nio.file.Files;
import java.security.MessageDigest;

public class PutObjectWithSha256 {
    public static void main(String[] args) {
        // 认证用的ak和sk硬编码到代码中或者明文存储都有很大的安全风险，建议在配置文件或者环境变量中密文存放，使用时解密，确保安全；本示例以ak和sk保存在环境变量中为例，运行本示例前请先在本地环境中设置环境变量ACCESS_KEY_ID和SECRET_ACCESS_KEY_ID。
        // 您可以登录访问管理控制台获取访问密钥AK/SK，获取方式请参见https://support.huaweicloud.com/usermanual-ca/ca_01_0003.html
        String ak = System.getenv("ACCESS_KEY_ID");
        String sk = System.getenv("SECRET_ACCESS_KEY_ID");
        // 【可选】如果使用临时AK/SK和SecurityToken访问OBS，同样建议您尽量避免使用硬编码，以降低信息泄露风险。
        // 您可以通过环境变量获取访问密钥AK/SK/SecurityToken，也可以使用其他外部引入方式传入。
        String securityToken = System.getenv("SECURITY_TOKEN");

        // endpoint填写桶所在的endpoint, 此处以华北-北京四为例，其他地区请按实际情况填写。
        // 您可以通过环境变量获取endPoint，也可以使用其他外部引入方式传入。
        // String endPoint = System.getenv("ENDPOINT");
        String endPoint = "https://obs.cn-north-4.myhuaweicloud.com";

        // 创建ObsClient实例
        try (ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint)) {
            // 本示例用于文件上传到examplebucket桶中的exampleObjectKey,并指定content-sha256头域。

            String buketName = "examplebucket";
            String objectKey = "exampleObjectKey";
            File localFile = new File("localFilePath");
            PutObjectRequest putObjectRequest = new PutObjectRequest();
            putObjectRequest.setBucketName(buketName);
            putObjectRequest.setObjectKey(objectKey);
            putObjectRequest.setFile(localFile);
            // 计算文件sha256
            InputStream fis = Files.newInputStream(localFile.toPath());
            byte[] buffer = new byte[1024];
            MessageDigest sha256 = MessageDigest.getInstance("SHA-256");
            for (int numRead = 0; (numRead = fis.read(buffer)) > 0; ) {
                sha256.update(buffer, 0, numRead);
            }
            fis.close();
            // 转为16进制
            StringBuilder sha256Builder = new StringBuilder();
            for (byte aB : sha256.digest()) {
                sha256Builder.append(String.format("%02x", aB));
            }
            // 添加文件sha256到自定义头域
            putObjectRequest.addUserHeaders("x-obs-content-sha256", sha256Builder.toString());
            obsClient.putObject(putObjectRequest);
            System.out.println("PutObjectWithSha256 successfully");
        } catch (ObsException e) {
            System.out.println("PutObjectWithSha256 failed");
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
            System.out.println("PutObjectWithSha256 failed");
            // 其他异常信息打印
            e.printStackTrace();
        }
    }
}
```

>![](public_sys-resources/icon-notice.gif) **须知：** 
>Java SDK 同时支持MD5与SHA256校验，在安全上更推荐使用SHA256算法。

